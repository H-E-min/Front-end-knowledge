## ES6

### 一、Generator 函数

1. Generator 函数组成

   Generator 有两个区分于普通函数的部分：

- 一是在 function 后面，函数名之前有个 * ；

- 函数内部有 yield 表达式。

  其中 * 用来表示函数为 Generator 函数，yield 用来定义函数内部的状态。

2. 执行机制

   调用 Generator 函数`在函数名后面加上()即可`，返回一个`指向内部状态对象的指针`，所以要调用遍历器对象Iterator 的 next 方法，指针就会从函数头部或者上一次停下来的地方开始执行。

   `{value: "1", done: false}`将yield 后边表达式的值 '1'，作为返回对象的 value 属性值，此时函数还没有执行完， 返回对象的 done 属性值是 false。

3. 函数返回的遍历器对象的方法

   **next 方法**

   一般情况下，`next 方法不传入参数`的时候，yield 表达式的`返回值是 undefined `。当 `next 传入参数`的时候，`该参数会作为上一步yield的返回值`。

   ```js
   function* sendParameter(){
       console.log("start");
       var x = yield '2';
       console.log("one:" + x);
       var y = yield '3';
       console.log("two:" + y);
       console.log("total:" + (x + y));
   }
   //不传参
   var sendp1 = sendParameter();
   sendp1.next();
   // start
   // {value: "2", done: false}
   sendp1.next();
   // one:undefined
   // {value: "3", done: false}
   sendp1.next();
   // two:undefined
   // total:NaN
   // {value: undefined, done: true}
   next传参
   var sendp2 = sendParameter();
   sendp2.next(10);
   // start
   // {value: "2", done: false}
   sendp2.next(20);
   // one:20
   // {value: "3", done: false}
   sendp2.next(30);
   // two:30
   // total:50
   // {value: undefined, done: true}
   ```

   **return 方法**

   return 方法返回给定值，并结束遍历 Generator 函数。

   return 方法提供参数时，返回该参数；不提供参数时，返回 undefined 。

   **yield\* 表达式**

   yield* 表达式表示 yield 返回一个遍历器对象，用于在 Generator 函数内部，调用另一个 Generator 函数。

   