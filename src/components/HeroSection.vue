<template>
  <section class="hero" ref="heroRef">
    <div class="hero-bg">
      <canvas ref="canvasRef" />
    </div>

    <div class="hero-content">
      <p class="tag" v-motion :initial="{ opacity: 0, y: 20 }" :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }">
        <span class="dot" />Available for opportunities
      </p>

      <h1 v-motion :initial="{ opacity: 0, y: 40 }" :enter="{ opacity: 1, y: 0, transition: { delay: 400 } }">
        <span class="line">Full Stack</span>
        <span class="line accent">Developer</span>
        <span class="line">& QA Engineer</span>
      </h1>

      <p class="desc" v-motion :initial="{ opacity: 0, y: 30 }" :enter="{ opacity: 1, y: 0, transition: { delay: 600 } }">
        I build reliable, production-ready web and mobile applications —
        from API design to deployment. Backend-focused with strong QA ownership.
      </p>

      <div class="ctas" v-motion :initial="{ opacity: 0, y: 20 }" :enter="{ opacity: 1, y: 0, transition: { delay: 800 } }">
        <a href="#projects" class="btn-primary">See my work →</a>
        <a href="#contact" class="btn-ghost">Get in touch</a>
      </div>

      <div class="stats" v-motion :initial="{ opacity: 0 }" :enter="{ opacity: 1, transition: { delay: 1000 } }">
        <div class="stat">
          <span class="stat-num">1+</span>
          <span class="stat-label">Years experience</span>
        </div>
        <div class="stat-divider" />
        <div class="stat">
          <span class="stat-num">70%</span>
          <span class="stat-label">Bug reduction at Daytruck</span>
        </div>
        <div class="stat-divider" />
        <div class="stat">
          <span class="stat-num">5+</span>
          <span class="stat-label">Projects shipped</span>
        </div>
      </div>
    </div>

    <div class="avatar-wrap" v-motion :initial="{ opacity: 0, scale: 0.8 }" :enter="{ opacity: 1, scale: 1, transition: { delay: 500 } }">
      <div class="avatar-blob">
        <span>ME</span>
      </div>
      <div class="avatar-ring r1" />
      <div class="avatar-ring r2" />
    </div>

    <div class="scroll-hint">scroll ↓</div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const canvasRef = ref(null)

onMounted(() => {
  const canvas = canvasRef.value
  const ctx = canvas.getContext('2d')
  let W = canvas.width = window.innerWidth
  let H = canvas.height = window.innerHeight

  window.addEventListener('resize', () => {
    W = canvas.width = window.innerWidth
    H = canvas.height = window.innerHeight
  })

  const particles = Array.from({ length: 60 }, () => ({
    x: Math.random() * W,
    y: Math.random() * H,
    r: Math.random() * 1.5 + 0.5,
    dx: (Math.random() - 0.5) * 0.4,
    dy: (Math.random() - 0.5) * 0.4,
    o: Math.random() * 0.4 + 0.1
  }))

  const draw = () => {
    ctx.clearRect(0, 0, W, H)
    particles.forEach(p => {
      ctx.beginPath()
      ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2)
      ctx.fillStyle = `rgba(200,255,0,${p.o})`
      ctx.fill()
      p.x += p.dx; p.y += p.dy
      if (p.x < 0 || p.x > W) p.dx *= -1
      if (p.y < 0 || p.y > H) p.dy *= -1
    })
    requestAnimationFrame(draw)
  }
  draw()
})
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex; align-items: center; justify-content: space-between;
  padding: 8rem 3rem 4rem;
  position: relative; overflow: hidden;
  gap: 2rem;
}
.hero-bg {
  position: absolute; inset: 0; z-index: 0;
  background: radial-gradient(ellipse 70% 60% at 70% 30%, rgba(200,255,0,0.04) 0%, transparent 60%);
}
canvas { position: absolute; inset: 0; width: 100%; height: 100%; }

.hero-content { position: relative; z-index: 1; max-width: 620px; }

.tag {
  display: inline-flex; align-items: center; gap: 0.5rem;
  font-family: 'DM Mono', monospace;
  font-size: 0.75rem; letter-spacing: 0.1em;
  color: var(--muted); margin-bottom: 2rem;
}
.dot {
  width: 7px; height: 7px; border-radius: 50%;
  background: var(--lime);
  animation: blink 2s infinite;
}
@keyframes blink {
  0%, 100% { opacity: 1; } 50% { opacity: 0.3; }
}

h1 {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: clamp(3rem, 7vw, 6.5rem);
  line-height: 0.95; letter-spacing: -0.04em;
  margin-bottom: 1.75rem;
}
.line { display: block; }
.accent { color: var(--lime); }

.desc {
  color: var(--muted); font-size: 1rem; line-height: 1.8;
  max-width: 480px; margin-bottom: 2.5rem;
}

.ctas { display: flex; gap: 1rem; flex-wrap: wrap; margin-bottom: 3rem; }

.btn-primary {
  background: var(--lime); color: var(--ink);
  padding: 0.9rem 2rem; border-radius: 100px;
  font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.9rem;
  text-decoration: none;
  transition: transform 0.2s, box-shadow 0.2s;
}
.btn-primary:hover { transform: translateY(-3px); box-shadow: 0 12px 32px rgba(200,255,0,0.3); }

.btn-ghost {
  border: 1.5px solid rgba(255,255,255,0.15); color: var(--white);
  padding: 0.9rem 2rem; border-radius: 100px;
  font-family: 'Syne', sans-serif; font-weight: 700; font-size: 0.9rem;
  text-decoration: none;
  transition: border-color 0.2s, transform 0.2s;
}
.btn-ghost:hover { border-color: var(--white); transform: translateY(-3px); }

.stats { display: flex; align-items: center; gap: 2rem; }
.stat { display: flex; flex-direction: column; gap: 0.2rem; }
.stat-num {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: 1.75rem; color: var(--lime); letter-spacing: -0.04em;
}
.stat-label { font-size: 0.75rem; color: var(--muted); }
.stat-divider { width: 1px; height: 40px; background: rgba(255,255,255,0.1); }

.avatar-wrap {
  position: relative; z-index: 1;
  width: clamp(220px, 28vw, 380px);
  height: clamp(220px, 28vw, 380px);
  flex-shrink: 0;
}
.avatar-blob {
  width: 100%; height: 100%;
  background: linear-gradient(135deg, var(--lime) 0%, var(--sky) 100%);
  border-radius: 40% 60% 55% 45% / 45% 55% 45% 55%;
  display: flex; align-items: center; justify-content: center;
  animation: morph 8s ease-in-out infinite;
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: clamp(2.5rem, 5vw, 4.5rem);
  color: var(--ink); letter-spacing: -0.04em;
}
.avatar-ring {
  position: absolute; border-radius: 50%;
  border: 1px solid rgba(200,255,0,0.15);
  animation: spin 20s linear infinite;
}
.r1 { inset: -20px; }
.r2 { inset: -45px; animation-direction: reverse; animation-duration: 30s; }

@keyframes morph {
  0%,100% { border-radius: 40% 60% 55% 45% / 45% 55% 45% 55%; }
  25% { border-radius: 55% 45% 40% 60% / 55% 45% 55% 45%; }
  50% { border-radius: 50% 50% 60% 40% / 40% 60% 50% 50%; }
  75% { border-radius: 45% 55% 45% 55% / 60% 40% 55% 45%; }
}
@keyframes spin { to { transform: rotate(360deg); } }

.scroll-hint {
  position: absolute; bottom: 2rem; left: 50%;
  transform: translateX(-50%);
  font-family: 'DM Mono', monospace; font-size: 0.7rem;
  color: var(--muted); letter-spacing: 0.1em;
  animation: bounce 2s infinite;
}
@keyframes bounce {
  0%,100% { transform: translateX(-50%) translateY(0); }
  50% { transform: translateX(-50%) translateY(6px); }
}

@media (max-width: 768px) {
  .hero { flex-direction: column; padding: 7rem 1.25rem 3rem; text-align: center; }
  .tag { justify-content: center; }
  .ctas { justify-content: center; }
  .stats { justify-content: center; }
  .avatar-wrap { width: 200px; height: 200px; }
  .desc { margin: 0 auto 2rem; }
}
</style>