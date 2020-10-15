<template>
  <div>
    <div id="centreLeft2Chart" style="width:4.125rem; height: 4.625rem;"></div>
  </div>
</template>

<script>
import echartMixins from "@/utils/resizeMixins";

export default {
  data() {
    return {
      chart: null
    };
  },
  mixins: [echartMixins],
  mounted() {
    this.draw();
  },
  methods: {
    draw() {
      this.$http.get("/getTimeParams").then((res) => {
        if (res.data.flag) {
          // 基于准备好的dom，初始化echarts实例
          this.chart = this.$echarts.init(document.getElementById("centreLeft2Chart"));

          let option = {
            tooltip: {
              formatter: '{a} <br/>{b} : {c}'
            },
            series: [
              {
                name: 'RMS',
                type: 'gauge',
                max: res.data.data.ampRmsAllow,
                detail: {formatter: '{value}'},
                data: [{value: res.data.data.ampRmsReal, name: '均方根值'}]
              }
            ]
          };
          this.chart.setOption(option);
        }
      })
    }
  },
  destroyed() {
    window.onresize = null;
  }
};
</script>

<style lang="scss" scoped>
</style>