<template>
  <div>
    <div id="centreLeft1Chart" style="width:4.25rem; height: 4rem;"></div>
  </div>
</template>

<script>
import echartMixins from "@/utils/resizeMixins";

export default {
  data() {
    return {
      chart: null,
      ampMaxReal: null,
      ampMaxAllow: null,
      ampAverageReal: null,
      ampAverageAllow: null,
      ampKurtosisReal: null,
      ampKurtosisAllow: null,
      ampSkewnessReal: null,
      ampSkewnessAllow: null,
      ampSqrtReal: null,
      ampSqrtAllow: null,
      ampPulseReal: null,
      ampPulseAllow: null
    };
  },
  mixins: [echartMixins],
  mounted() {
    this.draw();
  },
  methods: {
    // draw() {
    //   // 基于准备好的dom，初始化echarts实例
    //   this.chart = this.$echarts.init(document.getElementById("centreLeft1Chart"));
    //   //  ----------------------------------------------------------------
    //
    //   this.chart.setOption({
    //     color: [
    //       "#37a2da",
    //       "#32c5e9",
    //       "#9fe6b8",
    //       "#ffdb5c",
    //       "#ff9f7f",
    //       "#fb7293",
    //       "#e7bcf3",
    //       "#8378ea"
    //     ],
    //     tooltip: {
    //       trigger: "item",
    //       formatter: "{a} <br/>{b} : {c} ({d}%)"
    //     },
    //     toolbox: {
    //       show: true
    //     },
    //     calculable: true,
    //     legend: {
    //       orient: "horizontal",
    //       icon: "circle",
    //       bottom: 0,
    //       x: "center",
    //       data: ["rose1", "rose2", "rose3", "rose4", "rose5", "rose6"],
    //       textStyle: {
    //         color: "#fff"
    //       }
    //     },
    //     series: [
    //       {
    //         name: "增值电信业务统计表",
    //         type: "pie",
    //         radius: [10, 60],
    //         roseType: "area",
    //         center: ["50%", "40%"],
    //         data: [
    //           { value: 10, name: "rose1" },
    //           { value: 5, name: "rose2" },
    //           { value: 15, name: "rose3" },
    //           { value: 25, name: "rose4" },
    //           { value: 20, name: "rose5" },
    //           { value: 35, name: "rose6" }
    //         ]
    //       }
    //     ]
    //   });
    // }
    draw() {
      this.$http.get("/getTimeParams").then((res) => {
        if (res.data.flag) {
          this.ampMaxReal = res.data.data.ampMaxReal;
          this.ampMaxAllow = res.data.data.ampMaxAllow;
          this.ampAverageReal = res.data.data.ampAverageReal;
          this.ampAverageAllow = res.data.data.ampAverageAllow;
          this.ampKurtosisReal = res.data.data.ampKurtosisReal;
          this.ampKurtosisAllow = res.data.data.ampKurtosisAllow;
          this.ampSkewnessReal = res.data.data.ampSkewnessReal;
          this.ampSkewnessAllow = res.data.data.ampSkewnessAllow;
          this.ampSqrtReal = res.data.data.ampSqrtReal;
          this.ampSqrtAllow = res.data.data.ampSqrtAllow;
          this.ampPulseReal = res.data.data.ampPulseReal;
          this.ampPulseAllow = res.data.data.ampPulseAllow;

          // 基于准备好的dom，初始化echarts实例
          this.chart = this.$echarts.init(document.getElementById("centreLeft1Chart"));
          let dataBJ = [
            [this.ampMaxReal, this.ampAverageReal, this.ampKurtosisReal, this.ampSkewnessReal, this.ampSqrtReal, this.ampPulseReal],
            // [10, 10, 1, 10, 10, 10],
            // [20, 10, 1, 10, 10, 10],
            // [30, 10, 1, 10, 10, 10],
            // [40, 10, 1, 10, 10, 10],
            // [50, 10, 1, 10, 10, 10],
          ];

          let lineStyle = {
            normal: {
              width: 1,
              opacity: 0.5
            }
          };

          let option = {
            radar: {
              indicator: [
                { name: "峰值", max: this.ampMaxAllow },
                { name: "平均幅值", max: this.ampAverageAllow},
                { name: "峭度", max: this.ampKurtosisAllow },
                { name: "歪度", max: this.ampSkewnessAllow },
                { name: "方根幅值", max: this.ampSqrtAllow },
                { name: "脉冲指标", max: this.ampPulseAllow }
              ],
              shape: "circle",
              splitNumber: 5,
              name: {
                textStyle: {
                  color: "rgb(238, 197, 102)"
                }
              },
              splitLine: {
                lineStyle: {
                  color: [
                    "rgba(238, 197, 102, 0.1)"
                  ].reverse()
                }
              },
              splitArea: {
                show: false
              },
              axisLine: {
                lineStyle: {
                  color: "rgba(238, 197, 102, 0.5)"
                }
              }
            },
            series: [
              {
                name: "平均幅值",
                type: "radar",
                lineStyle: lineStyle,
                data: dataBJ,
                symbol: "none",
                itemStyle: {
                  normal: {
                    color: "#F9713C"
                  }
                },
                areaStyle: {
                  normal: {
                    opacity: 0.1
                  }
                }
              },
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