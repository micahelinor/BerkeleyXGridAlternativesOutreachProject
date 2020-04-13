<template>
  <div>
    <TreeChart :json="treeData" />
  </div>
</template>

<script>

  import TreeChart from "vue-tree-chart";
  import tree from "./json/tree.json";


  export default {
    components: {
      TreeChart
    },
    data () {
      return { 
        treeData: tree
    }
  }
}
</script>

