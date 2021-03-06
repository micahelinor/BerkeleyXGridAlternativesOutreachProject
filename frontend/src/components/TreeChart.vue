<template>
    <table v-if="treeData.name">
      <tr>
        <td :colspan="treeData.children ? treeData.children.length * 2 : 1" :class="{parentLevel: treeData.children, extend: treeData.children && treeData.extend}">
          <div :class="{node: true, hasMate: treeData.mate}">
            <div class="person" @click="$emit('click-node', treeData)"></div>
            <div class="name">
              <div class="button">
              <b-button aria-controls="collapse-4" @click="visible = !visible">
                <p>
                {{treeData.name}}
                </p>
              </b-button>
              </div>
                <b-collapse id="collapse-4" v-model="visible" class="mt-2">
                  <b-card v-if="treeData.projects">
                    <div class="collapse">
                    <p>Project Name: {{treeData.projects[0].projName}}</p>
                    <p>Grant Amount: {{treeData.projects[0].grantAmount}}</p>
                    <p>Date: {{treeData.projects[0].date}}</p>
                    <p>Geographic Location: {{treeData.projects[0].location}}<p>
                    <p>Contact: {{treeData.projects[0].contact}}</p>
                    </div>
                 </b-card>
                 <b-card v-if="treeData.info">
                   <div class="collapse">
                    <p>Contact: {{treeData.info[0].contact}}</p>
                    <p>Location: {{treeData.info[0].location}}</p>
                    <p>Role in Project: {{treeData.info[0].role}}</p>
                    </div>
                 </b-card>
                </b-collapse>
            </div>
          </div>
        <div class="extend_handle" v-if="treeData.children" @click="toggleExtend(treeData)"></div>
      </td>
    </tr>
    <tr v-if="treeData.children && treeData.extend">
      <td v-for="(children, index) in treeData.children" :key="index" colspan="2" class="childLevel">
        <TreeChart :json="children" @click-node="$emit('click-node', $event)"/>
      </td>
     </tr>
  </table>
</template>

<script>
export default {
  name: "TreeChart",
  props: ["json"],
  data() {
    return {
      treeData: {},
      visible: false
    }
  },
  watch: {
    json: {
      handler: function(Props){
        let extendKey = function(jsonData){
          jsonData.extend = (jsonData.extend===void 0 ? true: !!jsonData.extend);
          if(Array.isArray(jsonData.children)){
            jsonData.children.forEach(c => {
              extendKey(c)
            })
          }
          return jsonData;
        }
        if(Props){
          this.treeData = extendKey(Props);
        }
      },
      immediate: true
    }
  },
  methods: {
    toggleExtend: function(treeData){
      treeData.extend = !treeData.extend;
      this.$forceUpdate();
    }
  }
}
</script>

<style scoped>
table{border-collapse: separate!important;border-spacing: 0!important;}
td{position: relative; vertical-align: top;padding:0 0 50px 0;text-align: center; }

.extend_handle{position: absolute;left:50%;bottom:30px; width:10px;height: 10px;padding:10px;transform: translate3d(-15px,0,0);cursor: pointer;}
.extend_handle:before{content:""; display: block; width:100%;height: 100%;box-sizing: border-box; border:2px solid;border-color:#ccc #ccc transparent transparent;
transform: rotateZ(135deg);transform-origin: 50% 50% 0;transition: transform ease 300ms;}
.extend_handle:hover:before{border-color:#333 #333 transparent transparent;}
.extend .extend_handle:before{transform: rotateZ(-45deg);}

.extend::after{content: "";position: absolute;left:50%;bottom:15px;height:10px;border-left:2px solid #ccc;transform: translate3d(-1px,0,0)}
.childLevel::before{content: "";position: absolute;left:50%;bottom:100%;height:15px;border-left:2px solid #ccc;transform: translate3d(-1px,0,0)}
.childLevel::after{content: "";position: absolute;left:0;right:0;top:-15px;border-top:2px solid #ccc;}
.childLevel:first-child:before, .childLevel:last-child:before{display: none;}
.childLevel:first-child:after{left:50%;height:15px; border:2px solid;border-color:#ccc transparent transparent #ccc;border-radius: 6px 0 0 0;transform: translate3d(1px,0,0)}
.childLevel:last-child:after{right:50%;height:15px; border:2px solid;border-color:#ccc #ccc transparent transparent;border-radius: 0 6px 0 0;transform: translate3d(-1px,0,0)}
.childLevel:first-child.childLevel:last-child::after{left:auto;border-radius: 0;border-color:transparent #ccc transparent transparent;transform: translate3d(1px,0,0)}

.node{position: relative; display: inline-block;width: 9.5em;box-sizing: border-box; text-align: center;}
.node .person{position: relative; display: inline-block;z-index: 2;width:6em; overflow: hidden;}

.node .person .name{height:2em;line-height: 2em;overflow: hidden;width:100%;}
.button {
    width: 140px;
    height: px;
    border:0px solid #1b577d;
    background-color: #86C232;
    border-radius: 5px;
    padding-top: 1px;
    padding-bottom: 25px;
    
  }
  .button p{
    position: relative;
    top: 0.015px;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    font-size: 18px;
    text-align: center;
    vertical-align:middle;
  }
.collapse {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  font-size: 13px;
  border:px solid #D3D3D3;
  background-color: #09d81300;
  border-radius: 5px;
  text-align: left;

}
.node.hasMate::after{content: "";position: absolute;left:2em;right:2em;top:2em;border-top:2px solid #ccc;z-index: 1;}
.node.hasMate .person:last-child{margin-left:1em;}

.landscape{transform:translate(-100%,0) rotate(-90deg);transform-origin: 100% 0;}
.landscape .node{text-align: left;height: 8em;width:8em;}
.landscape .person{position: relative; transform: rotate(90deg);padding-left: 4.5em;height: 4em;top:4em;left: -1em;}
.landscape .person .avat{position: absolute;left: 0;}
.landscape .person .name{height: 4em; line-height: 4em;}
.landscape .hasMate{position: relative;}
.landscape .hasMate .person{position: absolute; }
.landscape .hasMate .person:first-child{left:auto; right:-4em;}
.landscape .hasMate .person:last-child{left: -4em;margin-left:0;}
</style>
