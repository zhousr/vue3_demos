<template>
  <div class="parent">
    <messageChild
      ref="oneRef"
      :propkey="parentValue"
      @emitEvent="getEmitValue"
      v-model="parentValue"
    />
    <p>parentValue：{{ parentValue }}</p>
    <div class="flex">
      <button @click="oneRef.childValue += '改_'">改子value</button>
    </div>
    <button @click="eventBus.emit('busParentToSun', parentValue)">eventBus</button>
  </div>
  <p>---{{ $attrs.attrKey }}???</p>
  <p>{{ cptPValue }}</p>
  <p @click="cptSet = 10000000000">{{ cptSet }}</p>
  <ul>
    <li v-for="(item, index) in arr" :key="index">{{ item }}</li>
  </ul>
  <ul>
    <li v-for="(item, index) in arr2" :key="index">{{ item }}</li>
  </ul>
</template>


<script setup lang="ts">
import messageChild from './messageChild.vue'
import { ref, useTemplateRef, onMounted, getCurrentInstance, computed, reactive } from 'vue'
import { eventBus } from './eventBus'
const parentValue = ref(10)

const getEmitValue = (value) => {
  console.log(value, 'emit')
  return value
}
// const arr = ref([1, 2, 3])
const arr = reactive([1, 2, [2, 2, 2]])
const [arr2] = arr
//
//第一种拿到ref
const oneRef: any = ref(null)
//第二种拿到ref
const twoRef: any = useTemplateRef('oneRef')
onMounted(() => {
  console.log(oneRef.value.childValue, '一')
  console.log(twoRef.value.childValue, '二')
  //第三种拿到ref
  console.log((getCurrentInstance() as any).ctx.$refs.oneRef.childValue, '三')
})

const cptPValue = computed(() => 'computed：' + parentValue.value)
const cptSet = computed({
  get: () => 555 + parentValue.value,
  set: (newVal) => (parentValue.value = newVal),
})
</script>


<style>
.parent {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>
