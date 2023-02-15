<template>
<!--  主页模块-->
  <div>
    <el-row :gutter="10" style="margin-bottom: 60px">
      <el-col :span="12">
        <el-card style="color: #409EFF">
          <div><i class="el-icon-user-solid"></i>用户总数</div>
          <div  style="padding: 10px 0;text-align: center;font-weight: bold" v-model="userOnline">
            {{userOnline}}
          </div>
        </el-card>
      </el-col>
      <el-col :span="12">
        <el-card style="color: #67C23A">
          <div><i class="el-icon-ice-cream-square"></i>文件总数</div>
          <div style="padding: 10px 0;text-align: center;font-weight: bold" v-model="fileOnline">
            {{ fileOnline }}
          </div>
        </el-card>
      </el-col>


    </el-row>

<!--    <h1>这是主页</h1>-->
    <el-row>
      <el-col :span="12">
        <div id="chart" style="width: 500px;height: 450px"></div>
      </el-col>
      <el-col :span="12">
        <div id="pie" style="width: 500px;height: 400px"></div>
      </el-col>
    </el-row>



  </div>

</template>

<script>

import * as echarts from 'echarts'



export default {
  name: "HomeView",
  data(){
    return{
      userOnline: '',
      fileOnline: '',
    }
  },
  created() {
    this.userAmount()
  },
  methods:{
    //显示用户总数
    userAmount(){
      this.request.get("/echarts/userOnline").then(res => {
        // console.log(res)
        this.userOnline = res.data
      })

      this.request.get("/echarts/fileOnline").then(res => {
        // console.log(res)
        this.fileOnline = res.data
      })
    },
  },
  mounted() {   //页面元素渲染之后再触发

    //折线图
    var option = {
      title: {
        text: '各季度注册用户人数',
        subtext: '趋势图',
        left: 'center',
      },
      tooltip: {
        trigger: 'item'
      },
      legend: {
        orient: 'vertical',
        left: 'left'
        // right: 'right',
      },
      xAxis: {
        type: 'category',
        data: ['第一季度','第二季度','第三季度','第四季度']
      },
      yAxis: {
        type: 'value'
      },
      series: [
        {
          name: "数量",
          data: [],
          type: 'bar',
        },
        {
          name: "数量 ",
          data: [],
          type: 'line'
        },
        // {
        //   name: "M记",
        //   data: [],
        //   type: 'bar'
        // },
        // {
        //   name: "M记",
        //   data: [],
        //   type: 'line'
        // },

      ]
    };


    //饼图
    var pieOption = {
      title: {
        text: '各地区人数数量统计',
        subtext: '比例图',
        left: 'center'
      },
      tooltip: {
        trigger: 'item'
      },
      legend: {
        orient: 'vertical',
        left: 'left'
      },
      series: [
        {
          name: '地区',
          type: 'pie',
          radius: '70%',
          label:{   //饼图图形上的文本标签
            normal:{
              show:true,
              position: "inner",  //标签的位置
              textStyle: {
                fontWeight: "bold",
                fontSize: 12 , //字体大小
                color: "black",
              },
              formatter: '{d}%'
            }
          },
          data: [], //填空
          emphasis: {
            itemStyle: {
              shadowBlur: 10,
              shadowOffsetX: 0,
              shadowColor: 'rgba(0, 0, 0, 0.5)'
            }
          }
        }
      ]
    };



    var chartDom = document.getElementById('chart');
    var myChart = echarts.init(chartDom);

    var pieDom = document.getElementById('pie');
    var pieChart = echarts.init(pieDom);


    this.request.get("/echarts/address").then(res => {
      pieOption.series[0].data = [
        {name: "广东" ,value: res.data[0]},
        {name: "上海" ,value: res.data[1]},
        {name: "北京" ,value: res.data[2]},
        {name: "香港" ,value: res.data[3]},
      ]

      pieChart.setOption(pieOption);
    })

    this.request.get("/echarts/members").then(res => {
      //填空
      // option.xAxis.data = res.data.x
      option.series[0].data = res.data
      option.series[1].data = res.data

      // option.series[2].data = [2,5,6,8]
      // option.series[3].data = [2,5,6,8]

      //在数据准备完毕之后在set
      myChart.setOption(option);

      // pieOption.series[0].data = [
      //   {name: "第一季度" ,value: res.data[0]},
      //   {name: "第二季度" ,value: res.data[1]},
      //   {name: "第三季度" ,value: res.data[2]},
      //   {name: "第四季度" ,value: res.data[3]},
      // ]
      //
      // pieChart.setOption(pieOption);
    })


  },

}
</script>

<style scoped>

</style>