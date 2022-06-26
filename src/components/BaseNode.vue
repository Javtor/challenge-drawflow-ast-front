<template>

  <div ref="el" @click="test">
    <div v-if="df">
      <div class="title">
        <h2>{{ name }}</h2>
      </div>
      <div class="ins">
        <p v-for="inputType in inputTypes">{{ inputType }}</p>
      </div>
      <div class="outs">
        <p v-for="outputType in outputTypes">{{ outputType }}</p>
      </div>
      <div class="content">
        {{ url }}
      </div>
    </div>
  </div>

</template>

<script>

import { getCurrentInstance, nextTick } from 'vue'

export default {
  data() {
    return {
      df: null,
      nodeId: 0
    }
  },
  props: ['name'],
  methods: {
    test() {
      console.log(this.df.getNodeFromId(this.nodeId))
    }
  },
  computed: {
    inputTypes() {
      return this.df.getNodeFromId(this.nodeId).data.inputTypes
    },
    url() {
      return this.df.getNodeFromId(this.nodeId).data.url
    },
    outputTypes() {
      return this.df.getNodeFromId(this.nodeId).data.outputTypes
    }
  },
  async mounted() {
    const internalInstance = getCurrentInstance()
    await nextTick()
    this.df = internalInstance.appContext.app._context.config.globalProperties.$df
    this.nodeId = this.$refs.el.parentElement.parentElement.id.slice(5)
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.title {
  position: absolute;
  vertical-align: top;
  margin-top: -15px;
  height: fit-content;
  left: 50%;
  top: 0%;
  transform: translate(-50%, 0%);
}

.ins {
  position: absolute;
  top: 50%;
  left: 0%;
  transform: translate(0%, -50%);
}

.outs{
  position: absolute;
  top: 50%;
  right: 0%; 
  transform: translate(0%, -50%);
}

.ins p, .outs p {
  height: 20px;
  margin-top: 19px;
  margin-bottom: 14px;
  padding: 0px 5px;
}


.content {
  position: absolute;
  text-align: center;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>
