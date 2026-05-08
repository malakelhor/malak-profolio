<template>
  <section id="contact">
    <div class="inner">
      <p class="label">Let's work together</p>
      <h2
        class="big"
        v-motion
        :initial="{ opacity: 0, y: 40 }"
        :visibleOnce="{ opacity: 1, y: 0 }"
      >
        Got a project<br/>in mind?<br/><span>Let's talk.</span>
      </h2>
      <p class="sub">Open to full-time roles, freelance, and remote opportunities.</p>

      <div class="links">
        <a href="mailto:malekelhor09@gmail.com" class="link email">
          <span class="dot" />malekelhor09@gmail.com
        </a>
        <a href="https://www.linkedin.com/in/malek-elhor-b4175926a/" target="_blank" class="link">
          LinkedIn ↗
        </a>
        <a href="https://github.com/malakelhor" target="_blank" class="link">
          GitHub ↗
        </a>
      </div>
    </div>

    <footer>
      <span>© 2025 Malek Elhor</span>
      <span>Built with Vue.js · Deployed on Vercel</span>
    </footer>
  </section>
</template>

<style scoped>
section {
  padding: 7rem 3rem 0;
  background: var(--ink2);
}
.inner { max-width: 800px; margin: 0 auto; padding-bottom: 7rem; }

.label {
  font-family: 'DM Mono', monospace;
  font-size: 0.72rem; color: var(--lime);
  letter-spacing: 0.2em; text-transform: uppercase;
  margin-bottom: 0.75rem;
}
.big {
  font-family: 'Syne', sans-serif;
  font-weight: 800; font-size: clamp(2.5rem, 7vw, 5.5rem);
  letter-spacing: -0.04em; line-height: 1;
  margin-bottom: 1.5rem;
}
.big span { color: var(--lime); }
.sub { color: var(--muted); margin-bottom: 3rem; font-size: 1rem; }

.links { display: flex; flex-wrap: wrap; gap: 1rem; }
.link {
  display: inline-flex; align-items: center; gap: 0.6rem;
  padding: 0.85rem 1.75rem; border-radius: 100px;
  border: 1.5px solid rgba(255,255,255,0.1);
  color: var(--white); text-decoration: none;
  font-family: 'DM Mono', monospace; font-size: 0.78rem;
  transition: all 0.2s;
}
.link:hover { border-color: var(--lime); color: var(--lime); transform: translateY(-2px); }
.link.email { border-color: rgba(200,255,0,0.3); }
.dot {
  width: 7px; height: 7px; border-radius: 50%;
  background: var(--lime); animation: blink 2s infinite;
}
@keyframes blink {
  0%,100% { opacity: 1; } 50% { opacity: 0.3; }
}

footer {
  border-top: 1px solid rgba(255,255,255,0.06);
  padding: 1.75rem 0;
  display: flex; justify-content: space-between;
  flex-wrap: wrap; gap: 1rem;
}
footer span {
  font-family: 'DM Mono', monospace;
  font-size: 0.7rem; color: var(--muted);
}

@media (max-width: 768px) {
  section { padding: 5rem 1.25rem 0; }
}
</style>