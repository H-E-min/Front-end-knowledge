## vue中使用echarts

#### 1.安装echarts包

```
cnpm install echarts --save
```

#### 2.引入到项目中

a.全局引入 （在main.js中引入）

```
import echarts from 'echarts'
Vue.prototype.$echarts = echarts
这种方法是直接绑定在vue实例上，所以在项目中任何页面，直接 this.$echarts 即可
```

b.局部引入（在所需页面引入）

```
import echarts from 'echarts'
```

#### 3.初始化echarts

a.首先在你需要echarts的页面中得创建一个dom元素

```
 <div id="myCharts" ref="myCharts"></div>
```

b.其次，在mounted中初始化echarts( `不能写在created中哦`)（ `以下例子为折线图`）

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
mounted(){
    以下三步即可完成echarts的初始化使用,代码注释的详解别忘了看看
   1.  const  myCharts = this.$echarts.init(this.$refs.myCharts);
   2.   let options = {
          title: { 
             text: '未来一周气温变化',   //图表顶部的标题 
             subtext: '纯属虚构'    //副标题
          },
          tooltip: {   //鼠标悬浮框的提示文字
              trigger: 'axis'
            },
          legend: {
            data:['最高气温','最低气温']
          },
          xAxis : [{  //x轴坐标数据
            type : 'category',
            boundaryGap : false,
            data : ['周一','周二','周三','周四','周五','周六','周日']
            }],
           yAxis : [{   //y轴坐标数据
              type : 'value',
              axisLabel : {
                formatter: '{value} °C'
              }
            }],
          series: [  //驱动图表生成的数据内容数组，几条折现，数组中就会有几个对应对象，来表示对应的折线
            {
              name:"最高气温",
              type: "line",  //pie->饼状图  line->折线图  bar->柱状图
              data:[11, 11, 15, 13, 12, 13, 10], 
              },
            {
              name:"最低气温",
              type: "line",  //pie->饼状图  line->折线图  bar->柱状图
              data:[1, -2, 2, 5, 3, 2, 0],
              }
          ]}

    3.  myCharts.setOption(options);
}
```

# 方式一、直接引入echarts

### 先npm安装echarts

```
npm install echarts --save
```

### 开发：

main.js

```
import myCharts from './comm/js/myCharts.js'
Vue.use(myCharts)
```

myCharts.js

```
/**
 * 各种画echarts图表的方法都封装在这里
 * 注意：这里echarts没有采用按需引入的方式，只是为了方便学习
 */

import echarts from 'echarts'
const install = function(Vue) {
    Object.defineProperties(Vue.prototype, {
        $chart: {
            get() {
                return {
                    //画一条简单的线
                    line1: function (id) {
                        this.chart = echarts.init(document.getElementById(id));
                        this.chart.clear();

                        const optionData = {
                            xAxis: {
                                type: 'category',
                                data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
                            },
                            yAxis: {
                                type: 'value'
                            },
                            series: [{
                                data: [820, 932, 901, 934, 1290, 1330, 1320],
                                type: 'line',
                                smooth: true
                            }]
                        };

                        this.chart.setOption(optionData);
                    },
                }
            }
        }
    })
}

export default {
    install
}
```

HelloWorld.vue

```
<template>
  <div class="hello">
    <div id="chart1"></div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
    }
  },
  mounted() {
    this.$chart.line1('chart1');
  }
}
</script>

<style scoped>
  #chart1 {
    width: 300px;
    height: 300px;
  }
</style>
```

![clipboard.png](https://segmentfault.com/img/bVbc22p?w=320&h=480)

# 方式二、使用[vue-echarts](https://github.com/Justineo/vue-echarts)

### 先npm安装vue-echarts

```
npm install echarts vue-echarts
```

### 开发：

除了全量引用echarts，我们还可以采用按需引入的方式

main.js

```
import ECharts from 'vue-echarts'
import 'echarts/lib/chart/line'
Vue.component('chart', ECharts)
```

HelloWorld.vue

```
<template>
  <div class="hello">
    <chart ref="chart1" :options="orgOptions" :auto-resize="true"></chart>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      orgOptions: {},
    }
  },
  mounted() {
    this.orgOptions = {
        xAxis: {
            type: 'category',
            data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
        },
        yAxis: {
            type: 'value'
        },
        series: [{
            data: [820, 932, 901, 934, 1290, 1330, 1320],
            type: 'line',
            smooth: true
        }]
    }
  }
}
    </script>
```

到这里就结束了。试过打包了，没报错~