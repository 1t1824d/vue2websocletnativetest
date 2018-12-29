<template>
  <div class="hello">  
<div id="myChart" :style="{width: '300px', height: '300px'}"></div>
   <websocket/>
  </div>
</template>

<script>
import websocket from "@/components/websocket"
export default {
  name: 'HelloWorld',
  components:{
    websocket
  },
  data () {
    return {
     
    }
  },
  mounted(){
      this.$axios
        .post("http://112.64.170.158:9117/Service1.svc/HistoryThermalData")
        .then(res => {
        console.log(res)
        })
        .catch(error => {
          console.log(error);
        });
          this.drawLine();
  },
 methods: {
    drawLine(){
        // 基于准备好的dom，初始化echarts实例
        let myChart = this.$echarts.init(document.getElementById('myChart'))
        // 绘制图表
        myChart.setOption({
            title: { text: '在Vue中使用echarts' },
            tooltip: {},
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
