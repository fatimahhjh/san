<!--  -->
<template>
  <div
    class="san"
    v-loading="loading"
    element-loading-text="拼命加载中"
    element-loading-spinner="el-icon-loading"
    element-loading-background="rgba(0, 0, 0, 0.8)"
  >
    <div class="mask">
      <el-card shadow="always" class="operation_box">
        <div class="showall_box">
          <el-button type="primary" size="mini" @click="showAll"
            >显示全部</el-button
          >
        </div>
        <div class="search_box">
          <el-input
            v-model="queryInfo.id"
            class="search"
            size="mini"
            placeholder="请输入要查找的内容"
          ></el-input>
          <el-button type="primary" size="mini" @click="showSpecific"
            >查找</el-button
          >
        </div>
      </el-card>
    </div>
    <div id="mynetwork"></div>
    <div class="scroll">
      <ul class="hint">
        <li>请</li>
        <li>在</li>
        <li>此</li>
        <li>处</li>
        <li>上</li>
        <li>下</li>
        <li>滑</li>
        <li>动</li>
      </ul>
    </div>
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
    return {
      nodeData: [],
      edgeData: [],
      // 获取指定交换机互联的参数对象
      queryInfo: {
        id: ""
      },
      loading: true
    };
  },

  watch: {},

  methods: {
    // 接口获取节点和关系
    getNodesEdges() {
      this.$http
        .get("getnodes")
        .then(res => {
          this.loading = false;
          let { edges, nodes } = res.data;
          this.initTopo(nodes, edges);
          this.nodeData = nodes;
          this.edgeData = edges;
        })
        .catch(res => {
          this.$message.error("数据获取失败");
        });
    },
    // 绘制拓扑图方法
    initTopo(nodes, edges) {
      var color = "gray";
      var len = undefined;
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
            size: 40,
            color: "#ffffff"
          },
          borderWidth: 2
        },
        edges: {
          width: 4,
          length: 300,
          font: {
            size: 30,
            color: "#ffffff"
          },
          smooth: {
            //设置两个节点之前的连线的状态
            enabled: false //设置为false之后，两个节点之前的连线始终为直线，不会出现贝塞尔曲线
          }
        },
        physics: {
          barnesHut: { gravitationalConstant: -20000 },
          stabilization: { iterations: 1000 }
        }
      };
      let network = new vis.Network(container, data, options);
    },
    // 展示全部交换机互联方法
    showAll() {
      this.getNodesEdges();
      this.initTopo(this.nodeData, this.edgeData);
    },
    // 查找指定交换机互联图
    showSpecific() {
      this.$http
        .get("getnodes", {
          params: this.queryInfo
        })
        .then(res => {
          console.log(res.data);
        })
        .catch(res => {
          this.$message.error("查找失败！");
        });
    }
  },
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {
    this.getNodesEdges();
  },
  watch: {},
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {}
};
</script>
<style lang="less" scoped>
//@import url(); 引入公共css类
body {
  color: #d3d3d3;
  font: 12pt arial;
  background-color: #404a5a;
}
.san {
  .mask {
    background-color: rgba(0, 0, 0, 0.3);
    position: fixed;
    top: 58px;
    width: 100%;
    margin: 0 auto;
    height: 70px;
    border-radius: 6px;
  }
  .scroll {
    width: 8%;
    // height: 100%;
    // background-color: rgba(0, 0, 0, 0.3);
    position: absolute;
    top: 19%;
    left: 93%;
    .hint {
      margin-top: 100px;
      li {
        margin-top: 20px;
        list-style: none;
        font-size: 15px;
        color: white;
      }
    }
  }
  .operation_box {
    background-color: rgba(0, 0, 0, 0.3);
    height: 69px;
    border: none;
    .showall_box {
      float: left;
      width: 120px;
    }
    .search_box {
      float: left;
      margin-left: 58px;
      .el-button--mini,
      .el-button--small {
        font-size: 12px;
        border-radius: 0px;
        margin-left: -6px;
      }
      .search {
        width: 200px;
      }
      /deep/.el-input--mini .el-input__inner {
        height: 28px;
        line-height: 28px;
        border-radius: 0px;
      }
    }
  }

  #mynetwork {
    width: 100%;
    height: 700px;
    background-color: #404a5a;
  }
  .el-row {
    margin-bottom: 20px;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
}
</style>
