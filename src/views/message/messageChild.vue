<template>
  <div class="child">
    <p>Props：{{ myProps.propkey }}</p>
    <div class="flex">
      <p class="flex">modelValue：</p>
      <input
        style="width: 100px"
        :value="myProps.modelValue"
        @input="myEmit('update:modelValue', $event?.target?.value)"
      />
    </div>
    <div>
      <button @click="reduceNum()">-</button>
      <input v-model="childValue" ref="myInput" />
      <button @click="addNum">+</button>
    </div>
    <button @click="myEmit('emitEvent', childValue)">emit</button>
    <messageSun :attrKey="childValue" style="color: red" />
  </div>
</template>

<script setup lang="ts">
import messageSun from './messageSun.vue'
import { ref, defineProps, provide } from 'vue'
const myProps = defineProps({
  propkey: Number,
  modelValue: Number,
})
const myEmit = defineEmits(['propkey: Number', 'update:modelValue', 'emitEvent'])
const childValue = ref(100)
const myInput = ref('')
//

provide('path96', childValue)
//
//
const addNum = () => {
  childValue.value++
}
const reduceNum = () => {
  childValue.value++
}

defineExpose({
  addNum,
  reduceNum,
  childValue,
})
</script>

<style scoped>
.child {
  padding: 100px;
  background-color: #eee;
  border: 2px solid red;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
input {
  margin: 0 10px;
}
</style>
