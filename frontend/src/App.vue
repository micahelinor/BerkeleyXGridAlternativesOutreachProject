<template>
  <div id="app">
    <label>
      切换为横向
      <input type="checkbox" v-model="landscape" value="1">
    </label>
    <TreeChart :json="data" :class="{landscape: landscape.length}" @click-node="clickNode" />
    <footer class="foot">
        <p>© 2020 - 3020 Authors
            <a href="https://github.com/micahelinor/BerkeleyXGridAlternativesOutreachProject" target="_blank">Kiana Kazemi & Micah Feras</a> 
            Github 
            <a href="https://github.com/micahelinor/BerkeleyXGridAlternativesOutreachProject" target="_blank">GRIDxBerkeley</a>
        </p>
    </footer>
  </div>
</template>

<script>
import TreeChart from "@/components/TreeChart";
import gridData from "./assets/data.json"

export default {
  name: 'app',
  components: {
    TreeChart
  },
  data() {
    return {
      landscape: [],
      data: gridData
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#app .avat{border-radius: 2em;border-width:2px;}
#app .name{font-weight:700;}
.foot {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    background: #333;
    padding: 24px;
    overflow: hidden;
    color: #999;
    font-size: 14px;
    text-align: center;
}
.foot a{color:#fff;margin:0 .5em}
</style>
