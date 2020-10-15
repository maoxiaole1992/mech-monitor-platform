<template>
  <div>
    <div id="centreRight2Chart1" style="width:3.25rem; height: 2.60rem;">123</div>
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
      // 基于准备好的dom，初始化echarts实例
      this.chart = this.$echarts.init(document.getElementById("centreRight2Chart1"));
      //  ----------------------------------------------------------------
      let dataBJ = [
        [94, 69, 114, 2.08, 73, 39, 22]
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
            { name: "平均幅值", max: 100 },
            { name: "峰值", max: 150 },
            { name: "峭度", max: 200 },
            { name: "歪度", max: 5 },
            { name: "方根幅值", max: 100 },
            { name: "脉冲指标", max: 100 }
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
          // {
          //   name: "峰值",
          //   type: "radar",
          //   lineStyle: lineStyle,
          //   data: dataSH,
          //   symbol: "none",
          //   itemStyle: {
          //     normal: {
          //       color: "#B3E4A1"
          //     }
          //   },
          //   areaStyle: {
          //     normal: {
          //       opacity: 0.05
          //     }
          //   }
          // },
          // {
          //   name: "峭度",
          //   type: "radar",
          //   lineStyle: lineStyle,
          //   data: dataGZ,
          //   symbol: "none",
          //   itemStyle: {
          //     normal: {
          //       color: "rgb(238, 197, 102)"
          //     }
          //   },
          //   areaStyle: {
          //     normal: {
          //       opacity: 0.05
          //     }
          //   }
          // }
        ]
      };
      this.chart.setOption(option);
    }
  },
  destroyed() {
    window.onresize = null;
  }
};
</script>

<style lang="scss" scoped>
#centreRight2Chart1 {
  margin: 0 auto;
}
</style>