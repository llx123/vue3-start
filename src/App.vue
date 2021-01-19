<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" @msgChange='msgChange'/>
  <TodoList />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import TodoList from './components/TodoList.vue'

export default defineComponent({
  name: 'App',
  components: {
    HelloWorld,
    TodoList
  },
  setup () {
    function msgChange (v: string) {
      console.log(v, 'msg from children')
    }

    return {
      msgChange
    }
  }
})
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
