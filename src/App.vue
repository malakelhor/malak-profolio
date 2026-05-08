<template>
  <div>
    <NavBar />
    <RouterView />
    <CursorGlow />
  </div>
</template>

<script setup>
import NavBar from './components/NavBar.vue'
import CursorGlow from './components/CursorGlow.vue'
</script>