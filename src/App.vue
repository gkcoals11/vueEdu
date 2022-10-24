<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <code-samples v-if="showComponent" msg="This is Vue 2 Syntax Sample"/>
    <button @click="onClick ">{{ showComponent ? '컴포넌트 닫기' : '컴포넌트 열기'}}</button>
  </div>
</template>

<script>
import CodeSamples from './components/CodeSamples.vue'

export default {
  name: 'App',
  components: {
    CodeSamples
  },
  data () {
    return {
      showComponent: true
    }
  },
  methods: {
    onClick () {
      this.showComponent === true ? this.showComponent = false : this.showComponent = true
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
