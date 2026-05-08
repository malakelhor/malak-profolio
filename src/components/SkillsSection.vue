<template>
  <section id="skills">
    <div class="inner">
      <p class="label">What I work with</p>
      <h2 class="title">Skills & Stack</h2>

      <div class="grid">
        <div
          v-for="(card, i) in skills" :key="i"
          class="card"
          :style="{ '--accent': card.color }"
          v-motion
          :initial="{ opacity: 0, y: 40 }"
          :visibleOnce="{ opacity: 1, y: 0, transition: { delay: i * 100 } }"
        >
          <div class="card-icon">{{ card.icon }}</div>
          <div class="card-title">{{ card.title }}</div>
          <div class="tags">
            <span v-for="tag in card.tags" :key="tag" class="tag">{{ tag }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const skills = [
  {
    icon: '⚙️', title: 'Backend', color: '#C8FF00',
    tags: ['Java', 'Spring Boot', 'Node.js', 'Laravel', 'CodeIgniter', 'REST APIs', 'JWT Auth', 'MVC']
  },
  {
    icon: '🎨', title: 'Frontend', color: '#00D4FF',
    tags: ['React.js', 'Next.js', 'Angular', 'JavaScript ES6+', 'HTML5', 'CSS3', 'Bootstrap']
  },
  {
    icon: '🗄️', title: 'Databases', color: '#FF5C3A',
    tags: ['MySQL', 'MongoDB', 'Relational Design']
  },
  {
    icon: '🧪', title: 'Testing & QA', color: '#9B6DFF',
    tags: ['PHPUnit', 'Unit Testing', 'Integration Testing', 'Manual Testing', 'Bug Tracking', 'Regression Testing']
  },
  {
    icon: '🛠️', title: 'Tools', color: '#C8FF00',
    tags: ['Git', 'Gitflow', 'Postman', 'Docker']
  },
  {
    icon: '🚀', title: 'Learning', color: '#00D4FF',
    tags: ['Kubernetes', 'CI/CD', 'AWS']
  }
]
</script>

<style scoped>
section {
  padding: 7rem 3rem;
  background: var(--ink2);
}
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
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1px;
  border: 1px solid rgba(255,255,255,0.06);
  border-radius: 20px; overflow: hidden;
}

.card {
  background: var(--ink2);
  padding: 2rem; position: relative;
  transition: background 0.2s;
  overflow: hidden;
}
.card::before {
  content: '';
  position: absolute; top: 0; left: 0; right: 0;
  height: 2px; background: var(--accent);
  transform: scaleX(0); transform-origin: left;
  transition: transform 0.3s;
}
.card:hover { background: var(--ink3); }
.card:hover::before { transform: scaleX(1); }

.card-icon { font-size: 1.6rem; margin-bottom: 0.75rem; }
.card-title {
  font-family: 'Syne', sans-serif;
  font-weight: 700; font-size: 1rem;
  margin-bottom: 1rem;
}
.tags { display: flex; flex-wrap: wrap; gap: 0.4rem; }
.tag {
  font-family: 'DM Mono', monospace;
  font-size: 0.68rem; padding: 0.25rem 0.65rem;
  border-radius: 100px;
  background: rgba(255,255,255,0.05);
  color: var(--muted);
  border: 1px solid rgba(255,255,255,0.07);
  transition: all 0.2s;
}
.card:hover .tag { color: var(--white); border-color: rgba(255,255,255,0.15); }

@media (max-width: 768px) {
  section { padding: 5rem 1.25rem; }
}
</style>