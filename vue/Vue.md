## 变化侦测篇

​		`变化侦测`可不是个新名词，它在目前的前端三大框架中均有涉及。在`Angular`中是通过`脏值检查流程`来实现变化侦测；在`React`是`通过对比虚拟DOM`来实现变化侦测，而在`Vue`中通过`Object.defineProperty`方法实现了对`object`数据的可观测，并且封装了`Observer`类，让我们能够方便的把`object`数据中的所有属性（包括子属性）都转换成`getter/seter`的形式来侦测变化。

### Object的变化侦测

1. ```
   Object.defineProperty(obj, prop, descriptor)
   //obj:要定义属性的对象。
   //prop:要定义或修改的属性的名称或 Symbol。
   //descriptor:要定义或修改的属性描述符。
   //返回值：被传递给函数的对象。
   ```

2. Observer模块

   Observer模块分为三个部分，也可以叫做三个类：

   ![image-20210107190309105](\Vue.assets\image-20210107190309105.png)

   ![image-20210107190337513](Vue.assets\image-20210107190337513.png)

   **`observer`类，它用来将一个`正常的object`转换成`可观测的object`，也可以叫数据监控对象。**

   `Dep类`：**依赖管理器。**

   `watcher类`：**订阅者对象。**

3. constructor

   **`constructor `**是一种用于创建和初始化`class`创建的对象的特殊方法。

4. `Object.keys(obj)`：参数：要返回其枚举自身属性的对象

   ​									  返回值：一个表示给定对象的所有可枚举属性的`字符串数组`

   **用法：**

   ![image-20210107193254224](D:Vue.assets\image-20210107193254224.png)
   
5. ### 何时收集依赖？何时通知依赖更新？

   ​		总结一句话就是：**在`getter`中调用了`dep.depend()`方法收集依赖，在`setter`中调用`dep.notify()`方法通知所有依赖更新。**

6.  Array. `splice()`和`slice()`

   `splice()` 方法向/从数组中添加/删除项目，然后`返回被删除的项目`。

   ​					注释：该方法会改变原始数组。

   `slice() `方法可从已有的数组中返回选定的元素。

   ​				使用方法:arr.slice(start,end);//start为初始位置,end为结尾位置,返回的结果是从start到end(不取)的新数组。

   ​				注释：不会改变原始数组。

   ​				如果调用slice()时，括号里什么都不写，那么则返回原数组。

7. `String.split()`和`Array.join()`

   `String.split()`：用于把一个`字符串分割成`字符串`数组`。

   `Array.join()`把`数组`中的所有元素放入一个`字符串`。

8. 语义化`谁用到了数据谁就是依赖`，`watcher`类的实例就是我们所说的谁，换句话说，就是谁用到了数据，谁就是依赖，就为谁创建一个`watcher`实例。

   ​		当数据变化时，我们就通知`Watcher`实例，由`Watcher`实例再去通知真正的依赖。

   ​		`Watcher`类的代码实现逻辑：`Watcher`先把自己设置到全局唯一的指定位置（`window.target`），然后读取数据。因为读取了数据，所以会触发这个数据的`getter`。接着，在`getter`中就会从全局唯一的那个位置读取当前正在读取数据的`Watcher`，并把这个`watcher`收集到`Dep`中去。收集好之后，当数据发生变化时，会向`Dep`中的每个`Watcher`发送通知。通过这样的方式，`Watcher`可以主动去订阅任意一个数据的变化。为了便于理解，我们画出了其关系流程图，如下图：

   ![img](https://vue-js.com/learn-vue/assets/img/3.0b99330d.jpg)

#### 总结

其整个流程大致如下：

1. `Data`通过`observer`转换成了`getter/setter`的形式来追踪变化。
2. 当外界通过`Watcher`读取数据时，会触发`getter`从而将`Watcher`添加到依赖中。
3. 当数据发生了变化时，会触发`setter`，从而向`Dep`中的依赖（即Watcher）发送通知。
4. `Watcher`接收到通知后，会向外界发送通知，变化通知到外界后可能会触发视图更新，也有可能触发用户的某个回调函数等。

### Array的变化侦测

1. ​	**Array型数据还是在getter中收集依赖。**

   **数组方法拦截器**

   ```javascript
   const arrayProto = Array.prototype
   // 创建一个对象作为拦截器
   export const arrayMethods = Object.create(arrayProto)
   
   // 改变数组自身内容的7个方法
   const methodsToPatch = [
     'push',
     'pop',
     'shift',
     'unshift',
     'splice',
     'sort',
     'reverse'
   ]
   
   /**
    * Intercept mutating methods and emit events
    */
   methodsToPatch.forEach(function (method) {
     const original = arrayProto[method]      // 缓存原生方法
     Object.defineProperty(arrayMethods, method, {
       //可枚举性（enumerable）用来控制所描述的属性,是否将被包括在for...in循环之中。具体来说，如果一个属性的enumerable为false，下面的操作不会取到该属性。
   	// for..in循环  ：只遍历对象自身的和继承的可枚举的属性
   	//Object.keys方法 ：返回对象自身的所有可枚举的属性的键名
   	//JSON.stringify方法：只串行化对象自身的可枚举的属性
       //Object.assign()(ES6）:只拷贝对象自身的可枚举的属性
       enumerable: false,
       //设置属性是否可以被删除,属性是否可更改；默认情况下为true,当我们设置为false时，属性值不可以被删除和修改
       configurable: true,
       //设置属性是否是可写的，当此值为false,则此属性为只读，缺省情况下，此属性值为true
       writable: true,
       value:function mutator(...args){
         const result = original.apply(this, args)
         return result
       }
     })
   })
   ```

   ![img](https://vue-js.com/learn-vue/assets/img/2.b446ab83.png)



