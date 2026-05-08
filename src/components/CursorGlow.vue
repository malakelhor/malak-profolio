<template>
  <div class="cursor" :style="{ left: x + 'px', top: y + 'px' }" />
  <div class="cursor-ring" :style="{ left: rx + 'px', top: ry + 'px' }" />
</template>

<script setup>
import { ref, onMounted } from 'vue'

const x = ref(0), y = ref(0)
const rx = ref(0), ry = ref(0)

onMounted(() => {
  document.addEventListener('mousemove', e => {
    x.value = e.clientX
    y.value = e.clientY
  })

  const animate = () => {
    rx.value += (x.value - rx.value) * 0.1
    ry.value += (y.value - ry.value) * 0.1
    requestAnimationFrame(animate)
  }
  animate()
})
</script>

<style scoped>
.cursor {
  width: 10px; height: 10px;
  background: var(--lime);
  border-radius: 50%;
  position: fixed; pointer-events: none;
  z-index: 9999;
  transform: translate(-50%, -50%);
  transition: width 0.2s, height 0.2s;
}
.cursor-ring {
  width: 40px; height: 40px;
  border: 1.5px solid rgba(200,255,0,0.4);
  border-radius: 50%;
  position: fixed; pointer-events: none;
  z-index: 9998;
  transform: translate(-50%, -50%);
}
@media (max-width: 768px) {
  .cursor, .cursor-ring { display: none; }
}
</style>