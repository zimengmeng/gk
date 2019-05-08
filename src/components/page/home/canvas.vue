<template>
   <div class="wrap">
     <div id="chart1" ref="chart" style="width:100%; height:675px;">
     </div>
     <span class="one">111</span>
     <span class="two"></span>
     <span class="three"></span>
     <span class="four"></span>
   </div>
</template>
<script>
let option = {
      tooltip: {
        trigger: 'axis',
        axisPointer: {
        type: 'none'
        }
      },
      color:['#EBCC1A'],
      grid: {
        top: "0",
        left: "0",
        right: "0",
        bottom: "0",
        containLabel: true
      },
    xAxis: {
        type: 'category',
        data: ['1', '2', '3', '4', '5', '6', '7','8','9'],
        boundaryGap: true,
        axisLine: {
            onZero: true,
            lineStyle: {
              type: 'dashed',
              color: '#00b4ff',
            }
          },
        axisTick: {
        //---坐标轴 刻度
        show: false, //---是否显示
        inside: true, //---是否朝内
        lengt:8,                    //---长度
        lineStyle: {
          //color:'red',          //---默认取轴线的颜色
          width: 1,
          type: "solid"
        }
      },
      axisLabel: {
        //---坐标轴 标签
        show: false, //---是否显示
        inside: false, //---是否朝内
        rotate: 0, //---旋转角度
        margin: 5 //---刻度标签与轴线之间的距离
        //color:'red',              //---默认取轴线的颜色
      },
      //背景虚线
       splitArea: {show: false},
            splitLine: {
              show: true,
              lineStyle: {
                type: 'dashed',
                color: '#0082c9'
              }
            }
    },
    yAxis: {
        type: 'value',
        data: ['1', '2', '3', '4', '5', '6', '7','8','9'],
         splitLine: {
          show: false
        },
         axisLine: {
        //---坐标轴 轴线
        show: false, //---是否显示

        //------------------- 箭头 -------------------------
        // symbol: ["none", "arrow"], //---是否显示轴线箭头
        // symbolSize: [8, 8], //---箭头大小
        // symbolOffset: [0, 7], //---箭头位置

        //------------------- 线 -------------------------
        axisLine: {
              lineStyle: {color: '#005078'}
            },
      },
      axisTick: {
        //---坐标轴 刻度
        show: false, //---是否显示
        inside: true, //---是否朝内
        lengt:1, //---长度
        lineStyle: {
          //color:'red',          //---默认取轴线的颜色
          width: 1,
          type: "solid"
        }
      },
      axisLabel: {
        //---坐标轴 标签
        show: false, //---是否显示
        inside: false, //---是否朝内
        rotate: 20, //---旋转角度
        margin: 5 //---刻度标签与轴线之间的距离
        //color:'red',              //---默认取轴线的颜色
      },
      //背景虚线
      //  splitArea: {show: false},
      //       splitLine: {
      //         show: true,
      //         lineStyle: {
      //           type: 'dashed',
      //           color: '#0082c9'
      //         }
      //       }
    },
    series: [
        {
            name: '',
            type: 'line',
            areaStyle: {color: '#0A2A53', opacity: 0.9},
            stack: 'two',
            lineStyle: {color: '#FFDF19', width: 5},
            yAxisIndex: 0,
            label: {
              show: false,
              fontSize: 16,
              position: 'top',
              color: '#009fe4'
            },
            itemStyle: {
              color: '#005aff',
              emphasis: {
                barBorderWidth: 5,
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowOffsetY: 0,
                shadowColor: 'rgba(0,0,0,0.5)'
              }
            },
            data: [200,80,250,90,350,120,450,250,300],
            //  data: [200,80,250,90,350,120,450,250,300],
            smooth: true,
      }]
};
import echarts from 'echarts'
export default {
  name:'Chart1',
   mounted() {
    let myChart = echarts.init(this.$refs.chart);
    myChart.setOption(option);
  }
}
</script>
<style scoped>
.wrap{
  width: 100%;
  height: 100%;
  position: relative;
}
 .one{
   display: inline-block;
   width: 20px;
   height: 20px;
   border-radius: 50%;
   background: red;
   position: absolute;
   top: 300px;
   left: 550px;
  }
   .two{
   display: inline-block;
   width: 20px;
   height: 20px;
   border-radius: 50%;
   background: blue;
   position: absolute;
   top: 150px;
   left: 950px;
  }
   .three{
   display: inline-block;
   width: 20px;
   height: 20px;
   border-radius: 50%;
   background: yellow;
   position: absolute;
   top: 450px;
   left: 1150px;
  }
   .four{
   display: inline-block;
   width: 20px;
   height: 20px;
   border-radius: 50%;
   background: orange;
   position: absolute;
   top: 60px;
   left: 1380px;
  }
</style>


