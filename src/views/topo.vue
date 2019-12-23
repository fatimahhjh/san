<!--  -->
<template>
  <div class="echartLayout">
    <div id="container" style="width:100%; height:100%; overflow:hidden;"></div>
  </div>
</template>

<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';
import echarts from "echarts";
export default {
  name: "SAN拓扑图",
  animation: "false",
  //import引入的组件需要注入到对象中才能使用
  components: {},
  data() {
    //这里存放数据
    return {
      myChart: null,
      chartData: [],
      chartLink: []
    };
  },
  //监听属性 类似于data概念
  computed: {},
  //监控data中的数据变化
  watch: {},
  //方法集合
  methods: {
    initEchart() {
      let dom = document.getElementById("container");
      this.myChart = echarts.init(dom);
      this.chartData = this.dataEChart();
      this.chartLink = this.linkEChart();
      let option = {
        tooltip: {
          show: false
        },
        series: [
          {
            edgeLabel: {
              normal: {
                formatter: "{c}",
                show: true
              }
            },
            edgeSymbol: "circle",
            force: {
              repulsion: 2000
            },
            layout: "force",
            roam: true,
            itemStyle: {
              normal: {
                color: "#4C8184"
              },
              //鼠标放上去有阴影效果
              emphasis: {
                shadowColor: "#3721db",
                shadowOffsetX: 0,
                shadowOffsetY: 0,
                shadowBlur: 40
              }
            },
            label: {
              normal: {
                show: true
              }
            },
            //添加到node里面的头像图片
            // symbol: `image://${imgSrc}`,
            symbolSize: 50,
            type: "graph",
            links: this.chartLink,
            data: this.chartData
          }
        ]
      };
      this.myChart.setOption(option);
      // this.myChart.on("click", function(params) {
      //   console.log(params.data);
      //获取点击的头像的数据信息
      // });
    },
    /**
     * 数据集合
     */
    dataEChart() {
      let data = [
        {
          name: "张1",
          id: "1"
        },
        {
          name: "张2",
          id: "2"
        },
        {
          name: "张3",
          id: "3"
        },
        {
          name: "张4",
          id: "4"
        },
        {
          name: "张5",
          id: "5"
        },
        {
          name: "张6",
          id: "6"
        },
        {
          name: "张7",
          id: "7"
        },
        {
          name: "张6",
          id: "8"
        }
      ];
      return data;
    },
    /**
     * 关系数据集合
     */
    linkEChart() {
      let dataLink = [
        { value: "同事", source: "1", target: "2" },
        { value: "同事", source: "1", target: "3" },
        { value: "同事", source: "1", target: "4" },
        { value: "同学", source: "1", target: "5" },
        { value: "同学", source: "1", target: "6" },
        { value: "同学", source: "1", target: "7" },
        { value: "", source: "3", target: "7" },
        { value: "爸爸", source: "1", target: "8" },
        { value: "妈妈", source: "2", target: "5" }
      ];
      return dataLink;
    }
  },
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {},
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {
    this.initEchart();
  }
};
</script>
<style lang='less' scoped>
//@import url(); 引入公共css类
.echartLayout {
  margin: auto;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}
</style>