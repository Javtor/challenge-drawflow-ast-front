<template>

  <header>
    <h3>Challenge Drawflow AST</h3>
  </header>
  <div class="container">
    <div class="col left">Col 1</div>
    <div class="col right">
      <div id="drawflow" @drop="drop($event)" @dragover="allowDrop($event)"></div>
    </div>
  </div>

</template>

<script>

import Drawflow from 'drawflow'
import styleDrawflow from 'drawflow/dist/drawflow.min.css'
import style from '../assets/style.css'
import { h, getCurrentInstance, render } from 'vue'
const Vue = { version: 3, h, render }

export default {
  data() {
    return {
      editor: null
    }
  },
  props: {
    msg: String
  },
  mounted() {
    const id = document.getElementById("drawflow");
    const internalInstance = getCurrentInstance()
    this.editor = new Drawflow(id, Vue, internalInstance.appContext.app._context);
    this.editor.start()

    var html = `
<div><p>Prueba</p><p>Prueba</p><p>Prueba</p><p>Prueba</p><p>Prueba</p><p>Prueba</p><p>Prueba</p><p>Prueba</p><p>Prueba</p><p>Prueba</p><p>Prueba</p><p>Prueba</p></div>
<style>p{
  height: 20px;
  margin-top: 19px;
    margin-bottom: 14px;
    margin-left:-10px;
    padding:0px;
    
}</style>
`;
    var data = { "name": '' };

    this.editor.addNode('github', 0, 1, 150, 300, 'github', data, html);
    this.editor.addNode('github', 1, 0, 800, 300, 'github', data, html);
    this.editor.on('connectionCreated', connection => {
      console.log(this.editor.getNodeFromId(connection.input_id));
      this.editor.addNodeInput(connection.input_id)
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #494949;
  padding: 0 20px;
}

.container {
  display: flex;
  flex-grow: 1;
  min-height: calc(100vh - 100px);
}

.col {
  margin: 0px;
  min-height: 100%;
}

.col.left {
  flex-basis: 250px;
  border-right: 1px solid #494949;
}

.col.right {
  flex-basis: 100px;
  flex-grow: 1;
}

.node {
  border-radius: 8px;
  border: 2px solid #494949;
  display: block;
  height: 60px;
  line-height: 40px;
  padding: 10px;
  margin: 10px 0px;
  cursor: move;

}

#drawflow {
  width: 100%;
  height: 100%;
  text-align: initial;
  background: #2b2c30;
  background-size: 20px 20px;
  background-image: radial-gradient(#494949 1px, transparent 1px);

}

a {
  color: #42b983;
}
</style>
