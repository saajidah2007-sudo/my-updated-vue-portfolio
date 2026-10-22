<script setup>
const skillGroups = [
  { category: "Frontend", items: ["HTML", "CSS", "JavaScript", "Vue.js", "Bootstrap"] },
  { category: "Backend", items: ["Node.js", "Express.js", "Python"] },
  { category: "Database", items: ["MySQL"] },
  { category: "Workflow", items: ["Git", "GitHub"] },
];
</script>

<template>
  <section id="skills" class="skills-section">
    <div class="section-heading skills-heading">
      <span class="skills-eyebrow">TOOLS IN THE KIT</span>

      <h2>
        A growing
        <span>toolkit.</span>
      </h2>

      <p>
        Technologies I've used while learning, collaborating, and building
        projects — no scorecards, just tools put to work.
      </p>
    </div>

    <div class="skills-container">
      <article
        v-for="group in skillGroups"
        :key="group.category"
        class="skill-card"
      >
        <div class="skill-card-top">
          <h3>{{ group.category }}</h3>
          <span class="skill-mark" aria-hidden="true"></span>
        </div>

        <ul class="skill-list">
          <li v-for="item in group.items" :key="item">{{ item }}</li>
        </ul>
      </article>
    </div>
  </section>
</template>