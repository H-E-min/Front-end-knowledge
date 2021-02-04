## 认识flow

### 简介

​	flow是`JavaScript静态类型检查工具`，Flow的工作方式：`类型推断`（通过变量的使用上下文来推断出变量类型，然后根据这些推断来检查类型）和`类型注释`（实现注释好期待的类型，Flow会基于这些注释来判断）。

**类型判断**

```
/*@flow*/

function split(str){
	return str.split(' ')
}

split(1)
//Flow检查上述代码后会报错，因为函数split期待的参数是字符串，而1是数字
```

**类型注释**

```
/*@flow*/

function add(x:number,y:number):number{
	return x+y
}

add(1,3)		//不报错
```

```
/*@flow*/

var arr:Array<number>=[1,2,3]
arr.push('hello')		//报错，因为数组中的每项应该均为数字
```

### flow在vue.js源码中的应用

​	在主目录下有个`.flowconfig`，它是Flow的配置文件，其中`[libs]`是用来`描述包含指定库定义的目录`。

> flow
>
> ——compiler.js			# 编译相关
>
> ——component.js	   #组件数据结构
>
> ——global-api.js		  #Global API结构
>
> ——modules.js		    #第三方库定义
>
> ——options.js			  #选项相关
>
> ——ssr.js					  #服务端渲染相关
>
> ——vnode.js			    #虚拟node相关
>
> ——weex.js				  #

## vue.js源码目录设计

> src
>
> ——compiler		# 编译相关
>
> ——core				# 核心代码
>
> ——platforms		#不同平台的支持
>
> ——server			   #服务端渲染
>
> ——sfc					# .vue文件解析
>
> ——shared			# 共享代码

### compiler

​	compiler目录`包含Vue.js所有编译相关的代码`，它包括把模板解析成ast语法树，ast语法树优化，代码生成等功能。

​	编译的工作可以在构建时做（借助webpack、vue-loader等辅助插件），也可以在运行时做，使用包含构建功能的Vue.js。显然，编译是一项耗性能的工作，所以更推荐前者——离线编译。

### core

​	core目录包含了`Vue.js的核心代码`，包括内置组件、全局API封装、Vue实例化、观察者、虚拟DOM、工具函数等等。

​	这里的代码可谓是Vue.js的灵魂，是重点分析的地方。

### platform

​	Vue.js是一个跨平台的MVVM框架，它`可以跑在web上`，也可以`配合weex跑在native客户端上`。`platform是Vue.js的入口`，2个目录代表2个主要入口，分别打包成运行在web上和weex上的Vue.js。

### server

​	Vue.js 2.0支持了服务端渲染，`所有服务端渲染相关的逻辑`都在这个目录下。注意：`这部分代码是跑在服务端的Node.js`，不要和跑在浏览器端的Vue.js混为一谈。

​	服务端渲染主要的工作是把组件渲染为服务器端的HTML字符串，将它们直接发送到浏览器，最后将静态标记"混合"为客户端上完全交互的应用程序。

### sfc

​	通常我们开发Vue.js都会借助webpack构建，然后通过.vue单文件编写组件。

​	这个目录下的代码逻辑会`把.vue文件内容解析成一个JavaScript的对象`。

### shared

​	Vue.js会定义一些工具方法，这里定义的工具方法都是会被`浏览器端的Vue.js和服务器端的Vue.js所共享的`。

## scripts目录

`config.js`

```js
const builds = {
  // Runtime only (CommonJS). Used by bundlers e.g. Webpack & Browserify
  'web-runtime-cjs-dev': {
    //表示构建的入口JS文件地址
    entry: resolve('web/entry-runtime.js'),
    //表示构建后的JS文件地址
    dest: resolve('dist/vue.runtime.common.dev.js'),
    //表示构建的格式		cjs表示遵循CommonJS规范、
    format: 'cjs',
    env: 'development',
    banner
  },
    'web-runtime-esm': {
    entry: resolve('web/entry-runtime.js'),
    dest: resolve('dist/vue.runtime.esm.js'),
    //es表示遵循ES Module规范
    format: 'es',
    banner
  },
   'web-runtime-dev': {
    entry: resolve('web/entry-runtime.js'),
    dest: resolve('dist/vue.runtime.js'),
    //umd遵循UMD规范
    format: 'umd',
    env: 'development',
    banner
  },
}
```

## vue的初始化过程

​	vue的定义：在core/instance/index.js，了解到通过Mixin方法给原型`挂载原型方法`，又通过initGlobalAPI给vue`挂载静态方法`。

## new Vue发生了什么

​	实际上是执行init方法，在init方法中，首先是对options的合并，接下来执行一系列初始化方法，还有响应式处理，在初始化的最后，如果检测到有el属性，则调用$mount去挂载vm。

## Vue实例（$mount）挂载的实现



​	