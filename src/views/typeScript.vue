<template>typeScript</template>


<script setup lang="ts">
interface obj {
  readonly myId: String | number // 只读属性
  strName?: string // 可选属性
  [abc: string]: any
}
var newObj: obj = {
  myId: 1,
  strName: 'asdfsdf',
  amy: 'asldfsd',
}
// console.log(newObj)

//数组和元组
const arr: number[] = [1, 2, 3, 3, 4]
arr.push(1, '2')
let yuanArr: [string, number] = ['str', 3, '1']
yuanArr.push('1', '2', 3)
console.log(yuanArr)

// 类型别名
type name = string
type xing = '周' | '邹' | '州'
function turnAllName(xing: xing, ming: name): name {
  return xing + ming
}
turnAllName('李', '树荣')
turnAllName('周', '树荣')
</script>


<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
