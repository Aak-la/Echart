# start
`npm install echarts --save`  
# children
```
<template>
  <div :style="chartStyle" ref="chart"></div>
</template>

<script>
import echarts from 'echarts';

export default {
  props: {
    options: {
      type: Object,
      required: true
    },
    chartStyle: {
      type: Object,
      default: () => ({ width: '100%', height: '400px' })
    }
  },
  data() {
    return {
      chart: null
    };
  },
  mounted() {
    this.initChart();
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$refs.chart);
      this.chart.setOption(this.options);
    }
  },
  watch: {
    options: {
      handler() {
        this.chart.setOption(this.options);
      },
      deep: true
    }
  },
  beforeDestroy() {
    if (this.chart) {
      this.chart.dispose();
    }
  }
};
</script>

```
# parent

```
<template>
  <div ref="chart" style="width: 100%; height: 400px;"></div>
</template>

<script>
import echarts from 'echarts';

export default {
  mounted() {
    const chartDom = this.$refs.chart;
    const chart = echarts.init(chartDom, null, { renderer: 'webgl' }); // 指定使用WebGL渲染引擎
    // 设置图表的配置项和数据
    const option = {
     
    };
    chart.setOption(option);
  },
};
</script>

<style>
/* 你的样式 */
</style>


```
# function
```
function isWebGLSupported() {
  // 创建一个canvas元素
  const canvas = document.createElement('canvas');
  // 尝试获取WebGL上下文，如果浏览器支持WebGL，getContext会返回一个WebGLRenderingContext对象
  const gl = canvas.getContext('webgl') || canvas.getContext('experimental-webgl');
  // 如果gl不为null，表示浏览器支持WebGL
  return gl !== null;
}

// 使用isWebGLSupported()函数来判断浏览器是否支持WebGL
if (isWebGLSupported()) {
  console.log('浏览器支持WebGL');
  // 在这里初始化使用WebGL的ECharts图表
} else {
  console.log('浏览器不支持WebGL');
  // 在这里初始化使用普通渲染引擎的ECharts图表
}

```
#  DNS预解析
```
module.exports = {
  chainWebpack: config => {
    config.plugin('html').tap(args => {
      // 修改或添加dnsPrefetch配置项
      args[0].dnsPrefetch = ['example.com', 'cdn.example.com'];
      return args;
    });
  }
};

```
