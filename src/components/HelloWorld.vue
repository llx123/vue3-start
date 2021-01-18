<template>
  <div class="hello">
    <input type="num" v-model="state.num1" @keyup="add">
    <input type="num" v-model="state.num2" @keyup="add">
    {{state.result}}
    {{state.result2}}
    <button type="button" @click="doEmit">Button</button>
  </div>
</template>

<script lang="ts">
import {
  defineComponent,
  ref,
  reactive,
  computed,
  onMounted,
  onUpdated,
  onUnmounted,
  onRenderTracked,
  onRenderTriggered
} from 'vue'

interface StateTest {
  num1: number;
  num2: number;
  [propName: string]: number;
}

export default defineComponent({
  name: 'HelloWorld',
  props: {
    msg: String
  },
  setup (props, { emit }) {
    onMounted(() => {
      console.log('onMounted', props)
    })
    onUpdated(() => {
      console.log('onUpdated')
    })
    onUnmounted(() => {
      console.log('onUnmounted')
    })
    onRenderTracked((e) => {
      console.log('onRenderTracked', e)
    })
    onRenderTriggered(() => {
      console.log('onRenderTriggered')
    })
    const state: StateTest = reactive({
      num1: 0,
      num2: 0,
      result: 0,
      result2: computed(() => +state.num1 + +state.num2)
    })

    const num1 = ref(0)
    const num2 = ref(0)
    const result = ref(0)
    function add () {
      // result.value = +num1.value + +num2.value
      state.result = +state.num1 + +state.num2
    }
    function doEmit () {
      emit('msgChange', 'newMas')
    }

    return {
      num1,
      num2,
      result,
      add,
      state,
      doEmit
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
