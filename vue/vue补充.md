## 一、`Vue`基础精讲

1. 每一个组件都是`Vue实例`。
2. 以`$`开头的都是`vue`的`实例属性或实例方法`。
3. 生命周期函数就是`vue实例`在某一个时间点会自动执行的函数。
4. 计算属性的`getter`和`setter`：

```vue
<template>
	<div>
     <!-- 插值表达式会先到data里面找，找不到就会去computed里面找 -->
    {{fullName}}
    </div>
</template>
<script>
    computed:{
    //当fullName为计算属性时，不需要在date里面定义，可以直接在页面展示
    fullName:{
      //读取内容
      get:function() {
        return  this.lastName + " " +  this.firstName
      },
      //修改内容
      set:function(value){
      // value就是要修改的值
      // split把字符串分割成数组
        var arr = value.split(' ')
        this.firstName = arr[1]
        this.lastName = arr[0]
      }
    }
  }
</script>		
```

5. `Vue`中的样式绑定	

   第一种：1.1 **class对象绑定样式**：是通过对class名的true和false来决定的

```vue
<template>
	<div>
        <font :class="{ColorObj:isRed}">哇哇哇</font>
    </div>
</template>

<script>
export default {
	data(){
        return{
            isRed:true
        }
    }
}
</script>

<style scoped>
.ColorObj{
  color:red
}
</style>
```

​		1.2 **class数组绑定样式**：是通过在数组里存放class名实现

```vue
<template>
	<div>
		<font :class="[isRed]">哇哇哇</font>
    </div>
</template>

<script>
export default {
	data(){
        return{
            isRed:'isRed'
        }
    }
}
</script>
<style scoped>
.isRed{
  color:red
}
</style>
```

​	第二种：2.1 **Style对象绑定样式**

```vue
<template>
	<div>
		<font :style="ColorObj">哇哇哇</font>
    </div>
</template>

<script>
export default {
	data(){
        return{
            ColorObj:{
                color:'red',
                fontSize:'50px'
            }
        }
    }
}
</script>
```

​		2.2 **Style数组绑定样式**（其实数组中放的也是对象）

```vue
<template>
	<div>
		 <font :style="[{color:'blue'},{fontSize:'30px'}]">哇哇哇</font>
    </div>
</template>

<script>
export default {
}
</script>
```

6.`key`使用场景一：

```vue
//表达“这两个元素是完全独立的，不要复用它们”
<template v-if="user">
      <label>用户名：</label>
      <input type="text" placeholder="请输入用户名" key="user-input">
</template>

<template v-else>
      <label>邮箱：</label>
      <input type="text" placeholder="请输入邮箱" key="email-input">
</template>

<button @click="fnClick">切换登录方式</button>

//在这个例子中是为了防止切换登录方式时 input的值不变
```

7.渲染列表的两种方式：

```vue
<template>
	<ul>
     <li v-for="(item,index) in [1,2,3,4]" :key="index">{{item}}--{{index}}</li>
   </ul>
   <ul>
     <li v-for="(item,key,index) of ObjList" :key="index">{{item}} -- {{key}} -- {{index}}
    </li>
</ul>
</template>
```

打印输出：

![image-20210118162903600](vue补充.assets\image-20210118162903600.png)

8.组件参数校验

```vue
<script>
export default {
  props:{
    content:{
      //可以是字符串或者数字
      type:[String,Number],
      //必填
      required:true,
      //默认值
      default:'default value',
      // value就是传入的内容,且长度必须大于5
      validator:function(value) {
          return (value.length > 5) 
      }
    }
  }
}
</script>
```

props特性：属性的传递不会在`dom`标签上显示，而且在子组件中可以通过`{{content}}`或`this.content`获取到值。

非props特性（子组件没有声明接受父组件传递过来的内容）：在子组件中不能使用传递过来的值，属性会展示在子组件最外层的`dom`标签的`html`属性里面。

9.给组件绑定原生事件

​	其中，在`vue`中，子组件监听的是原生事件，父组件监听的是自定义事件，想要触发父组件的事件，必须在子组件上`this.$emit`父组件的事件，当想要在父组件上触发原生事件时，可以通过`.native`执行。

```vue
<div-com @dblclick.native="fnClickDiv"></div-com>
```

10.非父子组件间传值（Bus|总线|发布订阅模式|观察者模式）

```js
//首先在main.js中
import Vue from 'vue'
Vue.prototype.$EventBus = new Vue()
```

```vue
//在需要监听的地方使用$on
//需要在生命周期 mounted 钩子函数里监听来自bus的事件change
  mounted(){
    var this_ = this
    this.$EventBus.$on('change',function(msg){
      this_.selfcontent = msg
    })
  },
```

```vue
//在需要递交的地方使用$emit
 handleChild(){
      this.$EventBus.$emit('change',this.selfcontent)
 },
```

```vue
//需要注意的是 要对监听的事件进行销毁 避免内存泄漏
 beforeDestroy () {
    console.log('销毁监听事件')
    this.$EventBus.$off('getNum')
 }
```

11.作用域插槽

应用场景：当子组件做循环或者在每个父组件中有不同的展示效果时使用作用域插槽；子组件可以向父组件传数据，父组件接收时必须通过`template`包裹，且用`slot-scope`接收数据

```vue
//父组件上，必须用template包裹，user相当于接受子组件传过来的内容，p标签：接受到user用p标签展示
<template>
	<div>
       <template slot="myUser" slot-scope="user"> 
            <p v-for="(item,index) in user.data" :key="index">
              {{item}}
            </p>
		</template>
    </div>
</template>
```

```vue
//子组件上
 <!-- 子组件使用:data绑定需要的值(data是自定义名字) -->
<slot  name="myUser" :data="user"></slot>
<script>
export default {
  data(){
    return {
      user:[
        {name:'jack',age:18},
        {name:'tom',age:19},
        {name:'jerry',age:20}
      ],
    }
  },
}
</script>
```

12.动态组件

```vue
<component :is="type"></component>
<button @click='fnChange'>切换组件</button>
<script>
	export default {
        data(){
            return {
                 type:'LiCom'
            }
        },
        methods:{
         	fnChange(){
      			this.type = this.type === 'LiCom' ? 'TableCom' : 'LiCom'
    		}
        }
    }
</script>
```

​	组件上绑定`v-once`，第一次被渲染的时候就会放入内存里，有效提高静态内容的展示效率（例如：切换组件时使用）

13. `Vue`中`css`动画原理

```vue
<template>
	<!-- 动画效果 -->
    <!-- transition包裹的内容会有一个过渡的动画效果  name可以任意的起-->
    <transition name="fade">
      <div v-if="show">hello world</div>
    </transition>
      <button @click="changeShow">切换</button>
</template>

<style>
/* 以fade开头是因为上面的DOM的Name是fade，默认的是以v开头 */
.fade-enter,
.fade-leave-to
{
  opacity: 0;
}
.fade-enter-active,
.fade-leave-active{
  transition: opacity 3s;
}
</style>
```

![img](https://img2018.cnblogs.com/blog/1709755/201909/1709755-20190924170738262-58943711.png)

![img](https://img2018.cnblogs.com/blog/1709755/201909/1709755-20190924170802923-847025979.png)

> **显示原理**：当一个元素被 **transition** 包裹了之后，vue会自动当分析元素的css样式，然后构建一个动画的流程，在动画即将被执行的一瞬间**(也就是事件触发后元素出现)**，vue会在内部标签上增加两个class名字，分别是 **fade-enter,fade-enter-active**,在动画执行到第二帧的时候，也就是动画开始后，**fade-enter**会变成 **fade-enter-to**,动画执行到最后到时候，vue会干一件事情，把之前添加到fade-enter-to,fade-enter-active这两个class去除掉**（如图1）**
>
> 在**第0s**的时候样式由**fade-enter控制，透明度为0**,当第二帧的时候，透明度在3s内由0到1过度，**如果transition的name不写，默认样式是v-enter, v-enter-active**
>
> ***隐藏原理：***当一个元素被**transition**包裹了之后，元素由显示到隐藏，是这样一个流程，在隐藏的第一个瞬间，**vue会给元素新增两个class，fade-leave,fade-leave-active**,在第二帧的时候，会把**fade-leave去掉，更新为fade-leave-to，**在最后的时候，会把**fade-leave-to,fade-leave-active**都去除掉**(事件执行元素消失)**
>
> 从动画开始到结束，**fade-leave-active**都存在，也就是在动画运行的过程中，**时刻监听着这个opacity这个属性，一旦opacity发生变化**，就让opacity在3s中慢慢的进行过度，在第一瞬间,也就是**fade-leave**的时候,opacity还是显示的，为1

14. `Vue`中使用`animate.css库`（利用的是`@keyframes`动画效果）

    > https://animate.style/#contributors 官网

    第一种引入：在`Index.html`引入

    ```html
    <link
        rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css"
    />
    ```

    第二种引入：

    ```shell
    npm install animate.css --save
    ```

    ```js
    //在main.js中：
    import animated from 'animate.css' 
    Vue.use(animated)
    ```

    使用：

    ```vue
    //vue模板中：
        <!-- 注意：必须使用animate__animated animate__开头，否则动画会无效 -->
    	<transition 
          name="fade"
          //进入动画效果
          enter-active-class="animate__animated animate__bounce"
         	//离开动画效果
          leave-active-class="animate__animated animate__flash"
        >
          <div v-if="show">hello world</div>
        </transition>
        <button @click="changeShow">切换</button>
    ```

    15. `vue`中设置初始动画

    ```vue
    <transition 
          //必须写appear
          appear
          //初始页面的动画效果
          appear-active-class="animate__animated animate__bounce"
        >
          <div v-if="show">hello world</div>
        </transition>
    ```

    16. `Vue`中同时使用`过渡`和`动画`

    ```vue
    <transition 
      	  //:duration=5000 自定义动画播放时长
          //{enter:3000,leave:5000}:入场和出场动画时间
          :duration="{enter:3000,leave:5000}"
          //type确定动画时长  type="transition"：将transition的时长作为动画时长
          type="transition"
          //过渡：animate__animated animate__heartBeat，动画：fade-enter-active
          enter-active-class="animate__animated animate__heartBeat fade-enter-active"
          leave-active-class="animate__animated animate__bounce fade-leave-active"
          appear-active-class="animate__animated animate__bounce"
    >
    <style scoped>
    .fade-enter,
    .fade-leave-to{
      opacity: 0;
    }
    .fade-enter-active,
    .fade-leave-active{
      transition: opacity 3s;
    }    
    </style>
    ```

    17. `Vue`中的`JS`动画与`velocity.js`

    ```vue
    //以下是简单的例子，还未和velocity结合使用
    //入场动画( @before-enter,@enter,@after-enter)
    //出场动画(@before-leave,@leave,@after-leave)
    <!-- @before-enter是内容由无到有的时候自动监听触发的函数 -->
          <!-- @enter是@before-enter触发结束后触发。 -->
          <!-- 元素enter事件中的done()执行完之后会触发after-enter事件 -->
          <transition 
           name="fade"
           @before-enter="handleBeforeEnter"
           @enter="handleEnter"
           @after-enter="handleAfterEnter"
          >
          	<div v-if="show">hello world</div>
          </transition>
          <button @click="changeShow">切换</button>
    export default {
    methods:{
        handleBeforeEnter(el){
          // el代表当前Dom元素
          el.style.color= 'red'
        },
        handleEnter(el,done){
          //el:元素；done:回调函数
          setTimeout(()=>{
            el.style.color = 'blue'
          },2000)
          setTimeout(()=>{
            done()
          },4000)
        },
        handleAfterEnter(el){
          el.style.color = 'black'
        },
    }
    ```

    18. `Vue`中多个元素的过渡

    ```vue
    <!-- mode="in-out" 先进入再隐藏  Out-in:先隐藏再显示-->
    //核心是给各个元素设置key
          <transition mode="out-in">
            <div v-if="show" key="hello">hello world</div>
            <div v-else key="bye">bye world</div>
          </transition>
          <button @click="changeShow">切换</button>
    
    <style scoped>
    .v-enter,.v-leave-to{
      opacity: 0;
    }
    .v-enter-active,.v-leave-active{
      transition: opacity 1s;
    }
    </style>
    ```

    `Vue`中多个组件的过渡

    ```vue
    //通过transition 和 is实现组件间切换动画
    <transition mode="in-out">
        <component :is="type"></component>
    </transition>
    ```

    ```vue
    //多个组件的过渡
    <transition-group>
            <div v-for="item in objs" :key="item.id">{{item.id}}--{{item.name}}</div>
    </transition-group>
          <button @click="fnAdd">添加成员</button>
    export default {
    	data(){
    		return {
    			objs:[
                    {name:'zhangsan',id:'1'},
                    {name:'lisi',id:'2'}
                ]
    		}
    	}
    }
    <script>
    methods:{
        fnAdd(){
          var length = this.objs.length
          length++ 
          this.objs.push({name:`新成员${length}`,id:`${length}`})
        },
    }
    </script>
    ```

    19. `Vue`的动画封装

    ```vue
    //在子组件中  通过js实现动画
    <template>
      <div>
        <transition
          @before-enter="handleBeforeEnter"
          @enter="handleEnter"
          @after-enter="handleAfterEnter"
        >
          <slot v-if="show"></slot>
        </transition>
      </div>
    </template>
    
    <script>
    export default {
      props:{
        show:''
      },
      methods:{
        handleBeforeEnter(el){
          el.style.color = 'red'
        },
        handleEnter(el,done){
          setTimeout(()=>{
            el.style.fontSize = '30px'
            done()
          },2000)
        },
        handleAfterEnter(el){
          el.style.color = 'yellow'
        }
      }
    }
    </script>
    ```

    ```vue
    //父组件
    <fade-com :show='show'>
            <div>hello world</div>
    </fade-com>
    <button @click="changeShow">切换</button>
    
    <script>
    export default{
        data(){
            return {
                show:true
            }
        }
    }
    </script>
    ```

    

