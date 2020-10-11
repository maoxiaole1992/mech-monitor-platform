<template>
  <div>
    <div id="bottomLeftChart" style="width:11.25rem;height:4.5rem;"></div>
  </div>
</template>

<script>
import echartMixins from "@/utils/resizeMixins";
export default {
  data() {
    return {
      chart: null,
      freqArr: [],
      ampArr:[]
    };
  },
  mixins: [echartMixins],
  mounted() {
    this.drawFreqDomain();
  },
  methods: {
    drawFreqDomain() {
        // 获取振动时域信息
      this.$http.get("/getFreqDomain").then((res) => {
          if (res.data.flag) {
              this.freqArr = res.data.data.freq;
              this.ampArr = res.data.data.amp;

              // 基于准备好的dom，初始化echarts实例
              this.chart = this.$echarts.init(document.getElementById("bottomLeftChart"));
              let option = {
                  tooltip: {
                      trigger: 'axis',
                      position: function (pt) {
                          return [pt[0], '10%'];
                      }
                  },
                  toolbox: {
                      feature: {
                          dataZoom: {
                              yAxisIndex: 'none'
                          },
                          restore: {},
                          saveAsImage: {}
                      }
                  },
                  xAxis: {
                      type: 'category',
                      boundaryGap: false,
                      data: this.freqArr
                  },
                  yAxis: {
                      type: 'value',
                      boundaryGap: [0, '20%']
                  },
                  dataZoom: [{
                      type: 'inside',
                      start: 0,
                      end: 50
                  }],
                  series: [
                      {
                          name: '幅值',
                          type: 'line',
                          smooth: true,
                          symbol: 'none',
                          sampling: 'average',
                          itemStyle: {
                              color: 'rgb(255,255,0)'
                          },
                          areaStyle: {
                              color: this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                  offset: 0,
                                  color: 'rgb(255, 70, 131)'
                              }, {
                                  offset: 0,
                                  color: 'rgb(255, 70, 131)'
                              }])
                          },
                          data: this.ampArr
                      }
                  ]
              };
              this.chart.setOption(option);
          }
      })
  },
  },
  destroyed() {
    window.onresize = null;
  }
};
</script>

<style lang="scss" scoped>
</style>