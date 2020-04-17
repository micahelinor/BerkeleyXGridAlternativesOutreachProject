<template>
  <v-stage ref="stage" :config="stageSize">
    <div id="app">
      <h1 class="header">
        California Air Resources Board Clean Vehicles Program Partners
      </h1>
    <TreeChart class="treeChart" :json="data" :class="{landscape: landscape.length}" @click-node="clickNode" />
    <footer class="foot">
        <p>© 2020 Authors
            <a href="https://github.com/micahelinor/BerkeleyXGridAlternativesOutreachProject" target="_blank">Kiana Kazemi, Micah Feras, and Emma Stephan</a> 
            Github 
            <a href="https://github.com/micahelinor/BerkeleyXGridAlternativesOutreachProject" target="_blank">GRIDxBerkeley</a>
        </p>
      </footer>
    </div>
  </v-stage>
  
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
      data: gridData,
      stage : {
        width: 0,
        height: 0
      }
    }
  },
  created() {
      window.addEventListener('resize', this.handleResize);
      this.handleResize();
  },
  destroyed() {
     window.removeEventListener('resize', this.handleResize);
  },
  methods: {
    handleResize() {
      this.stage.width = window.innerWidth;
      this.stage.height = window.innerHeight;
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
  color: #61892F;
  margin-top: 60px;
}
.header{
  position: absolute;
  top: 0;
  background: #00;
  padding: 30px;
  width: 100%;
  text-align: center;
  overflow: hidden;
}
.treeChart {
  position: absolute;
  top: 180px;

}
#app .avat{border-radius: 2em;border-width:2px;}
#app .name{font-weight:700;}
.foot {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    background: #222629;
    padding: 18px;
    overflow: hidden;
    color: #61892F;
    font-size: 12px;
    text-align: center;
}
.foot a{color:#fff;margin:0 .5em}
</style>
