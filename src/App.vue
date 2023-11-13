<script setup lang="ts">
import { ref, onMounted } from 'vue'

const move_x = ref(0)
const move_y = ref(0)
const window_width = ref(0)
const window_height = ref(0)
const clickArr = ref<{ x: number; y: number }[]>([])

function update(event) {
  move_x.value = event.pageX
  move_y.value = event.pageY
}
function onClicked(event) {
  clickArr.value.push({ x: event.pageX, y: event.pageY })
}

onMounted(() => {
  window.addEventListener('mousemove', update)
  window.addEventListener('mouseup', onClicked)
  window_width.value=window.innerWidth
  window_height.value=window.innerHeight
})
</script>

<template>
  <ul>
    <li>Windows width: {{ window_width }}, height: {{ window_height }}</li>
    <li>Mouse position is at: {{ move_x }}, {{ move_y }}</li>
    <li v-for="item in clickArr" :key="item.x">Mouse clicked at: {{ item.x }}, {{ item.y }}</li>
  </ul>
</template>
