<!--  -->
<template>
  <div id="san">
    <el-button class="selcetAll">默认按钮</el-button>
    <div id="mynetwork"></div>
  </div>
</template>

<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';
const vis = require("vis-network/dist/vis-network.min.js");
require("vis-network/dist/vis-network.min.css");
// import { DataSet, Network } from 'vis/index-network';
export default {
  //import引入的组件需要注入到对象中才能使用
  components: {},
  data() {
    //这里存放数据
    return {};
  },

  watch: {},
  //方法集合
  methods: {},
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {},
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {
    var color = "gray";
    var len = undefined;

    var nodes = [
      { id: 0, label: "0", group: 0 },
      { id: 1, label: "1", group: 0 },
      { id: 2, label: "2", group: 0 },
      { id: 3, label: "3", group: 1 },
      { id: 4, label: "4", group: 1 },
      { id: 5, label: "5", group: 1 },
      { id: 6, label: "6", group: 2 },
      { id: 7, label: "7", group: 2 },
      { id: 8, label: "8", group: 2 },
      { id: 9, label: "9", group: 3 },
      { id: 10, label: "10", group: 3 },
      { id: 11, label: "11", group: 3 },
      { id: 12, label: "12", group: 4 },
      { id: 13, label: "13", group: 4 },
      { id: 14, label: "14", group: 4 },
      { id: 15, label: "15", group: 5 },
      { id: 16, label: "16", group: 5 },
      { id: 17, label: "17", group: 5 },
      { id: 18, label: "18", group: 6 },
      { id: 19, label: "19", group: 6 },
      { id: 20, label: "20", group: 6 },
      { id: 21, label: "21", group: 7 },
      { id: 22, label: "22", group: 7 },
      { id: 23, label: "23", group: 7 },
      { id: 24, label: "24", group: 8 },
      { id: 25, label: "25", group: 8 },
      { id: 26, label: "26", group: 8 },
      { id: 27, label: "27", group: 9 },
      { id: 28, label: "28", group: 9 },
      { id: 29, label: "29", group: 9 }
    ];
    var edges = [
      { from: 1, to: 2, label: "描述" },
      { from: 2, to: 0 },
      { from: 4, to: 3 },
      { from: 5, to: 4 },
      { from: 4, to: 0 },
      { from: 7, to: 6 },
      { from: 8, to: 7 },
      { from: 7, to: 0 },
      { from: 10, to: 9 },
      { from: 11, to: 10 },
      { from: 10, to: 4 },
      { from: 13, to: 12 },
      { from: 14, to: 13 },
      { from: 13, to: 0 },
      { from: 16, to: 15 },
      { from: 17, to: 15 },
      { from: 15, to: 10 },
      { from: 19, to: 18 },
      { from: 20, to: 19 },
      { from: 19, to: 4 },
      { from: 22, to: 21 },
      { from: 21, to: 23 },
      { from: 23, to: 22 },
      { from: 22, to: 13 },
      { from: 25, to: 24 },
      { from: 26, to: 25 },
      { from: 25, to: 7 },
      { from: 28, to: 27 },
      { from: 29, to: 28 },
      { from: 28, to: 0 }
    ];

    // create a network
    var container = document.getElementById("mynetwork");
    var data = {
      nodes: nodes,
      edges: edges
    };
    var options = {
      nodes: {
        shape: "dot",
        size: 40,
        font: {
          size: 52,
          color: "#ffffff"
        },
        borderWidth: 2
      },
      edges: {
        width: 4,
        length: 300,
        font: {
          size: 52,
          color: "#ffffff",
          face: "Microsoft YaHei"
        },
        smooth: {
          //设置两个节点之前的连线的状态
          enabled: false //设置为false之后，两个节点之前的连线始终为直线，不会出现贝塞尔曲线
        }
      },
      physics: {
        barnesHut: { gravitationalConstant: -10000 },
        stabilization: { iterations: 1000 }
      }
    };
    let network = new vis.Network(container, data, options);
  }
};
</script>
<style lang="less" scoped>
//@import url(); 引入公共css类
body {
  color: #d3d3d3;
  font: 12pt arial;
  background-color: #222222;
}
#san {
  .selcetAll {
    position: absolute;
    top: 10px;
    left: 20px;
  }
  #mynetwork {
    width: 1350px;
    height: 500px;
    border: 1px solid #444444;
    background-color: #222222;
  }
}
</style>
