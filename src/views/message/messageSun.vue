<template>
  <div class="sun">
    <p>sunValue：{{ sunValue }}</p>
    <p>myInject：{{ myInject }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref, useAttrs, inject } from 'vue'
const sunValue = ref(1000)
// attrs
const attr: any = useAttrs()
console.log(Object.keys(attr), 'attr')
//
import { eventBus } from './eventBus'
eventBus.on('busParentToSun', (str) => {
  sunValue.value += str
})
const myInject = inject('path96')
</script>

<style>
.sun {
  padding: 10px;
  background-color: #eee;
  border: 2px solid blue;
  margin: 20px;
}
</style>
