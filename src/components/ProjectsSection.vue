<template>
  <section id="projects">
    <div class="inner">
      <p class="label">Things I built</p>
      <h2 class="title">Projects</h2>

      <div class="grid">
        <div
          v-for="(p, i) in projects" :key="i"
          class="card"
          :class="{ featured: p.featured }"
          v-motion
          :initial="{ opacity: 0, y: 50 }"
          :visibleOnce="{ opacity: 1, y: 0, transition: { delay: i * 120 } }"
          @mousemove="spotlight($event, i)"
        >
          <div class="card-top">
            <span class="num">0{{ i + 1 }}{{ p.featured ? ' — Featured' : '' }}</span>
            <div class="links">
              <a v-if="p.github" :href="p.github" target="_blank" class="link">
                <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.3 3.44 9.8 8.2 11.38.6.1.82-.26.82-.57v-2c-3.34.72-4.04-1.6-4.04-1.6-.54-1.38-1.33-1.75-1.33-1.75-1.08-.74.08-.72.08-.72 1.2.08 1.83 1.23 1.83 1.23 1.06 1.82 2.8 1.3 3.48.99.1-.77.4-1.3.74-1.6-2.67-.3-5.47-1.33-5.47-5.93 0-1.3.47-2.38 1.24-3.22-.14-.3-.54-1.52.1-3.18 0 0 1-.32 3.3 1.23a11.5 11.5 0 0 1 6 0c2.28-1.55 3.29-1.23 3.29-1.23.65 1.66.24 2.88.12 3.18.77.84 1.23 1.92 1.23 3.22 0 4.61-2.8 5.63-5.48 5.92.43.37.81 1.1.81 2.22v3.29c0 .32.2.68.82.57C20.56 21.8 24 17.3 24 12c0-6.63-5.37-12-12-12z"/></svg>
                GitHub
              </a>
              <a v-if="p.live" :href="p.live" target="_blank" class="link live">
                Live ↗
              </a>
            </div>
          </div>

          <h3>{{ p.title }}</h3>
          <p class="desc">{{ p.desc }}</p>

          <div class="stack">
            <span v-for="t in p.stack" :key="t" class="stag">{{ t }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const projects = [
  {
    featured: true,
    title: 'API Health Monitor',
    desc: 'Full stack dashboard for monitoring API endpoint uptime and response times. Pings endpoints, stores history in MongoDB, and visualizes health with color-coded status cards and response time charts.',
    stack: ['Node.js', 'Express', 'MongoDB', 'React', 'Recharts', 'Railway', 'Vercel'],
    github: 'https://github.com/malakelhor/health-monitor',
    live: 'https://health-monitor-lyart.vercel.app'
  },
  {
    title: 'Booking System API',
    desc: 'RESTful API for a booking platform with CRUD operations, input validation, and error handling. Built with Spring Boot backend and React frontend during internship at BenYounes Web.',
    stack: ['Spring Boot', 'React', 'MySQL', 'REST API'],
    github: 'https://github.com/malakelhor'
  },
  {
    title: 'Complaint Tracker',
    desc: 'Web application for tracking and managing customer complaints with full backend logic, data validation and consistency checks built in PHP and MySQL.',
    stack: ['PHP', 'MySQL', 'HTML/CSS'],
    github: 'https://github.com/malakelhor'
  }
]

const spotlight = (e, i) => {
  const card = e.currentTarget
  const rect = card.getBoundingClientRect()
  card.style.setProperty('--mx', ((e.clientX - rect.left) / rect.width * 100) + '%')
  card.style.setProperty('--my', ((e.clientY - rect.top) / rect.height * 100) + '%')
}
</script>

<style scoped>
section { padding: 7rem 3rem; background: var(--ink); }
.inner { max-width: 1100px; margin: 0 auto; }

.label {
  font-family: 'DM Mono', monospace;
  font-size: 0.72rem; color: var(--lime);
  letter-spacing: 0.2em; text-transform: uppercase;
  margin-bottom: 0.75rem;
}
.title {
  font-family: 'Syne', sans-serif;
  font-weight: 800; font-size: clamp(2rem, 5vw, 3.5rem);
  letter-spacing: -0.03em; margin-bottom: 3.5rem;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 1.25rem;
}

.card {
  border: 1px solid rgba(255,255,255,0.07);
  border-radius: 20px; padding: 2rem;
  background: var(--ink2); position: relative;
  overflow: hidden;
  transition: transform 0.25s, border-color 0.25s, box-shadow 0.25s;
}
.card::after {
  content: '';
  position: absolute; inset: 0; pointer-events: none;
  background: radial-gradient(circle at var(--mx,50%) var(--my,50%), rgba(200,255,0,0.05) 0%, transparent 60%);
  opacity: 0; transition: opacity 0.3s;
}
.card:hover { transform: translateY(-6px); border-color: rgba(200,255,0,0.25); box-shadow: 0 24px 60px rgba(0,0,0,0.5); }
.card:hover::after { opacity: 1; }
.card.featured { border-color: rgba(200,255,0,0.15); }

.card-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.25rem; }
.num {
  font-family: 'DM Mono', monospace;
  font-size: 0.7rem; color: var(--lime); letter-spacing: 0.08em;
}
.links { display: flex; gap: 0.75rem; }
.link {
  font-family: 'DM Mono', monospace;
  font-size: 0.72rem; color: var(--muted);
  text-decoration: none; display: flex; align-items: center; gap: 0.3rem;
  transition: color 0.2s;
}
.link svg { width: 13px; height: 13px; }
.link:hover { color: var(--white); }
.link.live { color: var(--lime); }
.link.live:hover { color: var(--white); }

h3 {
  font-family: 'Syne', sans-serif;
  font-weight: 700; font-size: 1.2rem;
  letter-spacing: -0.02em; margin-bottom: 0.75rem;
}
.desc { color: var(--muted); font-size: 0.88rem; line-height: 1.75; margin-bottom: 1.5rem; }

.stack { display: flex; flex-wrap: wrap; gap: 0.4rem; }
.stag {
  font-family: 'DM Mono', monospace; font-size: 0.67rem;
  padding: 0.22rem 0.6rem; border-radius: 4px;
  background: rgba(200,255,0,0.07); color: var(--lime);
  border: 1px solid rgba(200,255,0,0.12);
}

@media (max-width: 768px) {
  section { padding: 5rem 1.25rem; }
}
</style>