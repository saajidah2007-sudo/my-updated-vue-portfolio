<script setup>
import { ref } from "vue";

const pikachuSaysHi = ref(false);

const highlights = [
  {
    title: "Full-Stack Development",
    description: "Vue.js, Node.js, Express, PHP, and MySQL",
  },
  {
    title: "UI/UX Design",
    description: "Figma, wireframes, and thoughtful interfaces",
  },
  {
    title: "Cybersecurity",
    description: "Cisco certified security fundamentals",
  },
  {
    title: "Data Science",
    description: "Cisco certified data analysis foundations",
  },
];
</script>

<template>
  <section id="about" class="about-section">
    <header class="about-heading">
      <span class="section-tag">ABOUT ME</span>
      <h2 class="section-title">Trainer Profile</h2>
    </header>

    <div class="pokedex-container">
      <aside class="pikachu-welcome-card" aria-label="Trainer profile data">
        <div class="pikachu-sprite-container">
          <button
            class="pikachu-mascot"
            type="button"
            :aria-label="pikachuSaysHi ? 'Pikachu says hello' : 'Say hello to Pikachu'"
            @click="pikachuSaysHi = !pikachuSaysHi"
          >
            <svg viewBox="0 0 88 88" aria-hidden="true" focusable="false">
              <path d="M20 22 11 2 32 14 38 23M55 20 76 3 72 28 61 32" fill="#facc15" stroke="#713f12" stroke-width="3" stroke-linejoin="round" />
              <path d="m17 9 10 8-7 2ZM68 11 59 19 69 21Z" fill="#27272a" />
              <path d="M23 24 31 18 55 19 65 28 66 49 58 60 30 59 20 49 19 34Z" fill="#fde047" stroke="#713f12" stroke-width="3" stroke-linejoin="round" />
              <path d="M29 36h5v3h-5m19 0h5v-3h-5" fill="#27272a" />
              <path d="m38 44 5 3 5-3" fill="none" stroke="#713f12" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" />
              <circle cx="24" cy="45" r="5" fill="#ef4444" />
              <circle cx="61" cy="45" r="5" fill="#ef4444" />
              <path d="m30 58 8 2-2 11H25l-2-4Zm18 1 8-3 7 9-3 6H47Z" fill="#facc15" stroke="#713f12" stroke-width="2.5" stroke-linejoin="round" />
              <path d="m59 63 10-4 3 5 8-3 3 5-9 8-10-2Z" fill="#facc15" stroke="#713f12" stroke-width="2.5" stroke-linejoin="round" />
              <path d="m30 69 8 1-2 9H23l2-6Zm19 0 8-1 5 7-3 3H46Z" fill="#facc15" stroke="#713f12" stroke-width="2.5" stroke-linejoin="round" />
            </svg>
          </button>
        </div>

        <p class="pikachu-speech-bubble" aria-live="polite">
          {{ pikachuSaysHi ? "Pika-pika! Let's build something great!" : "Pika-pika! Welcome to my trainer profile!" }}
        </p>

        <div class="terminal-screen" aria-label="Trainer metadata">
          <div class="terminal-row"><span class="terminal-label">NAME</span><strong>Saajidah Abrahams</strong></div>
          <div class="terminal-row"><span class="terminal-label">ROLE</span><strong>Junior Web Developer</strong></div>
          <div class="terminal-row"><span class="terminal-label">ACADEMY</span><strong>Life Choices</strong></div>
          <div class="terminal-row"><span class="terminal-label">LOCATION</span><strong>Cape Town, SA</strong></div>
        </div>
      </aside>

      <div class="about-bio-content">
        <span class="about-bio-eyebrow">TRAINER BIO</span>
        <h3>Building thoughtful experiences for the web.</h3>
        <p>
          I’m a junior web developer trained at <strong>Life Choices Academy</strong>,
          with a foundation in front-end development and back-end logic. I enjoy building
          full-stack applications that balance technical stability with clear, thoughtful design.
        </p>
        <p>
          From creating wireframes in Figma to building Vue interfaces and API routes with
          Node.js, Express, PHP, and MySQL, I focus on making useful experiences for real people.
          Projects like RentoSphere and HRFlow have helped me grow as a developer and collaborator.
        </p>
        <p>
          I enjoy the mix of logic and creativity in development. I break problems into manageable
          steps, learn from feedback, and keep improving. I’m working toward a junior role where I
          can contribute to a team while growing as a full-stack developer.
        </p>

        <div class="about-highlights" aria-label="Skills and credentials">
          <article v-for="highlight in highlights" :key="highlight.title" class="highlight-card">
            <h4 class="highlight-title">{{ highlight.title }}</h4>
            <p class="highlight-desc">{{ highlight.description }}</p>
          </article>
        </div>
        <p class="about-focus-line"><strong>INTERESTS</strong> UI/UX · APIs · Full-stack web applications</p>
      </div>
    </div>
  </section>
</template>
