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
  <div>
    <echarts-component :options="chartOptions" :chart-style="chartStyle" />
  </div>
</template>

<script>
import EChartsComponent from '@/path/to/ECharts.vue';

export default {
  components: {
    EChartsComponent
  },
  data() {
    return {
      chartOptions: {
        // ECharts 配置项
        // ...
      },
      chartStyle: {
        width: '100%',
        height: '400px'
      }
    };
  }
};
</script>

```
