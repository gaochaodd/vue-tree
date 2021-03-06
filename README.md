[![npm](https://img.shields.io/npm/v/vue-tree-halower.svg )](https://www.npmjs.com/package/vue-tree-halower)
[![npm](https://img.shields.io/npm/dm/vue-tree-halower.svg)](https://www.npmjs.com/package/vue-tree-halower)
[![GitHub stars](https://img.shields.io/github/stars/halower/vue-tree.svg?style=social&label=Stars&style=for-the-badge)](https://github.com/halower/vue-tree/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/halower/vue-tree.svg?style=social&label=Fork&style=for-the-badge)](https://github.com/halower/vue-tree/network)
[![license](https://img.shields.io/github/license/mashape/apistatus.svg)]()

`
The document is poorly written and you are welcome to refine your documentation in the process of using it to better help others.
`
## Last Version Update Log
  adjusted some style problems, perfected the demo 
### (Version 1.5.4)
1. fix bugs that are not selected by some nodes in the radio mode caused by the previous version (1.5.3) 
2. perfect Domo Example
### (Version 1.5.3)
1. add  ```canDeleteRoot``` option to support the removal of root nodes
2. fix the ```async``` Invalid bug of the first level node
### (Version 1.5.2)
add a ```node-check``` event, ande remove ```nodeChecked``` event， because the ```nodeChecked``` event may be bubbling
# Version: 2.x  ([中文文档](https://github.com/halower/vue2-tree/blob/master/README_CN.md))
```QQ Group: 255965810``` <br/>
`we guess you may also see` [version 1.0](https://github.com/halower/vue2-tree/tree/1.x)
# Online Demo
[https://halower.github.io/vue-tree](http://120.77.84.4/)

# SelectTree API (2018-4-15)
 The latest release has the ability to support the dropdown tree, extending the following with the same basic attributes and events (consistent with the [Tree API](https://github.com/halower/vue-tree#tree-api-doc)) 
 
| Parameters | Description | Type | Optional value |Default value |
|---------- |-------- |---------- |---------- |---------- |
|searchable | Search Functionality Required | Boolean | Y |true |
|pleasechoosetext | Dropdown box default prompts this article | String | Y |Please choose ... |
|searchtext | Search box default prompts this article | String | Y |Search ... | 
|searchfilter | Custom search pull down tree filter function | Function | Y |Node => mode.title.indexOf (This.searchworld) > 1 | 
 ## Effect Chart (no demo here, other effects like Onlinedemo)
![](https://github.com/halower/vue-tree/blob/master/screenshots/selectTree.png)
### How to use
Please read the [Tree API](https://github.com/halower/vue-tree#tree-api-doc) documentation before using the selectTree
```
import { VTree, VSelectTree } from 'vue-tree-halower'
Vue.use (VTree)
Vue.use (VSelectTree)
 -------------------
<v-select-tree :data='treeData' v-model="['node-1-2']"/>
 ```
# Tree API Doc
### Node Property
| Parameters | Description | Type | Optional values | Default value |
|---------- |-------- |---------- |---------- |---------- |
|id | when this property is empty, the title property will be used as the key | String | Y | -|
|title | node name | String | N | -|
|children | child nodes | Array[object] | Y | -|
|async | whether to load child nodes asynchronously | Boolean | Y | false |
|expanded | node Expansion | Boolean | Y | false |
|halfcheck | whether the node is half optional (subordinate selected) | Boolean | Y | false |
|visible | is the node visible | Boolean | Y | true |
|selected | whether the node is selected | Boolean | Y | false |
|checked | whether the node check box is selected | Boolean | Y | false |
|nocheck | specifies that a node does not render check box when multiple checkboxes are open | Boolean | Y | false |
|loading | open load effect | Boolean | Y | false |
|chkDisabled | disable the function of a check box for a node | Boolean | Y | false |

### Tree Property
| Parameters | Description | Type | Optional values | default value |
|---------- |-------- |---------- |---------- |---------- |
|data | tree Data Source | Array[object] | N | -|
|multiple | turn on Check mode | Boolean | Y | false |
|tpl | custom templates | JSX | Y | false |
|halfcheck | turn on semi-select mode | Boolean | Y | select all |
|scoped | quarantine node Selected state | Boolean | Y | false |
|draggable | support drag? | Boolean | Y | false |
|dragafterexpanded | ro expand after dragging | Boolean | Y | true |
|canDeleteRoot |  can delete the root node  | Boolean | Y | false |
### method
| Method name | Description | Parameters |
|---------- |-------- |---------- |
| getSelectedNodes | returns an array of currently selected nodes | - |
| getCheckedNodes | returns the array of nodes selected by the current check box | - |
| getNodes |the options objects such as {selected:true}, if empty, use {} | options|
| searchNodes | filter:function/string (if it is a function, it will eventually return a Boolean type) |node|

### events
| Event name | Description | Parameters |
|---------- |-------- |---------- |
| node-click | click the node to trigger the event | node: Object |
| node-check | click the checkbox to trigger the event | node: Object, checked: boolean |
| node-mouse-over | over the node to trigger the event | node: Object |
| async-load-nodes | event used to implement asynchronous loading | node: Object |
| drag-node-end | drag node end trigger the event | {dragNode: Object, targetNode: Object} |
### How to use

Step1: install plugins
```
npm install babel-plugin-syntax-jsx babel-plugin-transform-vue-jsx babel-helper-vue-jsx-merge-props babel-preset-env --save-dev

npm install vue-tree-halower  --save
```
Step2: In your .babelrc
```
{
  "presets": ["env"],
  "plugins": ["transform-vue-jsx"]
}
```
Step3： In your main.js
```
import 'vue-tree-halower/dist/halower-tree.min.css' // you can customize the style of the tree
import VTree from 'vue-tree-halower'

Vue.use(VTree)
```


### Demo

`Html`
```
  <v-tree ref='tree' :data='treeData' :multiple='true' :tpl='tpl' :halfcheck='true'/>
     <input type="text" v-model="searchword" />
    <button type="button" @click="search">GO</button>
```
`JS`
```
<template>
 <div>
    <div class="tree-block">
      <input class="tree-search-input" type="text" v-model="searchword" placeholder="search..."/>
      <button class=" tree-search-btn" type="button" @click="search">search</button>
      <v-tree ref='tree1' :canDeleteRoot="true" :data='treeData1' :draggable='true' :tpl='tpl' :halfcheck='true' :multiple="true"/>
    </div>
   <div  class="tree-block"><v-tree ref="tree2" :data='treeData2' :multiple='false' @node-check='nodechekced' @async-load-nodes='asyncLoad2'/></div>
    <div  class="tree-block"> <v-select-tree :data='treeData3' v-model='initSelected' :multiple="true"/></div>
   
 </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      searchword: '',
      initSelected: ['node-1'],
      treeData1: [{
        title: 'node1',
        expanded: true,
        children: [{
          title: 'node 1-1',
          expanded: true,
          children: [{
            title: 'node 1-1-1'
          }, {
            title: 'node 1-1-2'
          }, {
            title: 'node 1-1-3'
          }]
        }, {
          title: 'node 1-2',
          children: [{
            title: "<span style='color: red'>node 1-2-1</span>"
          }, {
            title: "<span style='color: red'>node 1-2-2</span>"
          }]
        }]
      }],
      treeData2: [{
        title: 'node1',
        expanded: false,
        async: true
      }],

      treeData3: [{
        title: 'node1',
        expanded: true,
        children: [{
          title: 'node 1-1',
          expanded: true,
          children: [{
            title: 'node 1-1-1'
          }, {
            title: 'node 1-1-2'
          }, {
            title: 'node 1-1-3'
          }]
        }]
      }]
    }
  },
  methods: {
    nodechekced (node, v) {
      alert('that a node-check envent ...' + node.title + v)
    },
    tpl (node, ctx) {
      let titleClass = node.selected ? 'node-title node-selected' : 'node-title'
      if (node.searched) titleClass += ' node-searched'
      return <span>
        <button class="treebtn1" onClick={() => this.$refs.tree1.addNode(node, {title: 'sync node'})}>+</button>

         <span class={titleClass} domPropsInnerHTML={node.title} onClick={() => {
           this.$refs.tree1.nodeSelected(node)
         }}></span>
      <button class="treebtn2" onClick={() => this.asyncLoad1(node)}>async</button>
      <button class="treebtn3" onClick={() => this.$refs.tree1.delNode(node.parent, node)}>delete</button>
      </span>
    },
    async asyncLoad1 (node) {
      this.$set(node, 'loading', true)
      let pro = new Promise((resolve, reject) => {
        setTimeout(resolve, 2000, ['async node1', 'async node2'])
      })
      this.$refs.tree1.addNodes(node, await pro)
      this.$set(node, 'loading', false)
    },
    async asyncLoad2 (node) {
      this.$set(node, 'loading', true)
      let pro = await new Promise((resolve, reject) => {
        setTimeout(resolve, 2000, [{title: 'test1', async: true}, {title: 'test2', async: true}, {title: 'test3'}])
      })

      pro.forEach((el) => {
        if (!node.hasOwnProperty('children')) {
          this.$set(node, 'children', [])
        }
        node.children.push(el)
      })
      this.$set(node, 'loading', false)
    },
    search () {
      this.$refs.tree1.searchNodes(this.searchword)
    }
  }
}
</script>
<style>
.tree-block{
  float: left;
  width: 33%;
  padding: 10px;
  box-sizing: border-box;
  border: 1px dotted #ccccdd;
  overflow: auto;
  height: 800px;
}
.treebtn1{
  background-color: transparent;
  border: 1px solid #ccc;
  padding: 1px 3px;
  border-radius: 5px;
  margin-right: 5px;
  color: rgb(148, 147, 147);

}
.treebtn2{
   background-color: transparent;
   border: 1px solid #ccc;
   padding: 3px 5px;
   border-radius: 5px;
   margin-left: 5px;
  color: rgb(97, 97, 97);

}
.treebtn3{
 background-color: transparent;
 border: 1px solid #ccc;
 padding: 3px 5px;
 border-radius: 5px;
 margin-left: 5px;
  color: rgb(63, 63, 63);

}
.tree-search-input{
  width: 70%;
  padding: 6px 8px;
  outline: none;
  border-radius: 6px;
  border:1px solid #ccc;
}
.tree-search-btn{
width: 25%;
padding: 6px 8px;
outline: none;
border-radius: 6px;
background-color: rgb(218, 218, 218);
border:1px solid rgb(226, 225, 225);
color: rgb(117, 117, 117);
}
</style>

```
### 如果你觉得这个项目帮助到了你，你可以帮作者买一杯果汁表示鼓励
<img src="https://github.com/halower/vue2-tree/blob/master/src/assets/hello.png" width=256 height=256 />
