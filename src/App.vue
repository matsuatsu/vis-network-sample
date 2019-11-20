<template>
  <div id="app">
    <div id="mynetwork"></div>
  </div>
</template>

<script>
/* eslint-disable no-console */
import vis from "vis";

export default {
  name: "app",
  mounted: function() {
    // create an array with nodes
    let nodes = new vis.DataSet([
      { id: 1, label: "Node 1", value: 1 },
      { id: 2, label: "Node 2", value: 3 },
      { id: 3, label: "Node 3", value: 2 },
      { id: 4, label: "Node 4", value: 4 }
    ]);

    // create an array with edges
    let edges = new vis.DataSet([
      { from: 1, to: 3, label: "Edge 1" },
      { from: 1, to: 2, label: "Edge2" },
      { from: 2, to: 4, label: "Edge3" }
    ]);

    // create a network
    let container = document.getElementById("mynetwork");

    // provide the data in the vis format:
    let data = {
      nodes: nodes,
      edges: edges
    };

    let options = {
      nodes: {
        shape: "dot",
        scaling: {
          customScalingFunction: function(min, max, total, value) {
            return value / total;
          },
          min: 3,
          max: 5
        }
      }
    };

    // initialize your network!
    var network = new vis.Network(container, data, options);
    network.on("click", function(params) {
      if (params.nodes.length == 1) {
        var nodeId = params.nodes[0];
        var node = nodes.get(nodeId);
        console.log(node.label + "がクリックされました");
      } else if (params.edges.length == 1) {
        var edgeId = params.edges[0];
        var edge = edges.get(edgeId);
        console.log(edge.label + "がクリックされました");
      }
    });
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#mynetwork {
  border: 1px solid black;
  height: 500pt;
}
</style>
