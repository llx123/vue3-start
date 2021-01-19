<template>
  <div>
    <h2 @click="showRef" ref="testRef">TodoList</h2>
    <ul>
      <li v-for="(item, index) in lists"
      :key="index"
      v-show="!item.checked"
      @dblclick="showEdit(index)"
      >
        {{ item.name }}
      </li>
    </ul>
    <h3>Finish</h3>
    <ul>
      <li v-for="(item, index) in finish" :key="index" @click="item.checked = !item.checked">
        {{ item.name }}
      </li>
    </ul>
    <button @click="add">添加</button>
  </div>
</template>

<script lang="ts">
import { ref, reactive, toRefs, computed } from 'vue'
export default {
  setup () {
    const state = reactive({
      lists: [
        {
          name: '111'
        },
        {
          name: '222'
        }
      ],
      finish: computed(() => state.lists.filter(item => item.checked)),
      add: () => {
        state.lists.push({
          name: 'llx'
        })
      },
      showEdit: (i) => {
        console.log(i)
      },
      testRef: ref(null),
      showRef: (e) => {
        console.log(state.testRef, e.target.contains(state.testRef))
      }
    })

    return toRefs(state)
  }
}
</script>

<style lang="less">

</style>
