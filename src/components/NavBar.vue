<template>
  <nav :class="{ scrolled }">
    <a href="#" class="logo">ME.</a>
    <ul class="links">
      <li><a href="#skills">Skills</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
    <a href="mailto:malekelhor09@gmail.com" class="hire-btn">Hire me</a>
  </nav>
</template>

<script setup>
import { ref, onMounted } from 'vue'
const scrolled = ref(false)
onMounted(() => {
  window.addEventListener('scroll', () => {
    scrolled.value = window.scrollY > 50
  })
})
</script>

<style scoped>
nav {
  position: fixed; top: 0; left: 0; right: 0;
  padding: 1.5rem 3rem;
  display: flex; align-items: center; justify-content: space-between;
  z-index: 100;
  transition: all 0.3s;
}
nav.scrolled {
  padding: 1rem 3rem;
  background: rgba(8,8,8,0.85);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255,255,255,0.05);
}
.logo {
  font-family: 'Syne', sans-serif;
  font-weight: 800; font-size: 1.2rem;
  color: var(--lime); text-decoration: none;
}
.links {
  display: flex; gap: 2.5rem; list-style: none;
}
.links a {
  font-family: 'DM Mono', monospace;
  font-size: 0.78rem; letter-spacing: 0.08em;
  color: var(--muted); text-decoration: none;
  transition: color 0.2s;
}
.links a:hover { color: var(--white); }
.hire-btn {
  font-family: 'Syne', sans-serif;
  font-weight: 700; font-size: 0.82rem;
  padding: 0.6rem 1.4rem;
  border-radius: 100px;
  background: var(--lime); color: var(--ink);
  text-decoration: none;
  transition: transform 0.2s, box-shadow 0.2s;
}
.hire-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 24px rgba(200,255,0,0.3);
}
@media (max-width: 768px) {
  nav { padding: 1rem 1.25rem; }
  .links { display: none; }
}
</style>