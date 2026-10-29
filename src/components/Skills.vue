<script setup>
import { computed, ref } from "vue";

const skillGroups = [
  { category: "Frontend", filter: "frontend", items: ["HTML5", "CSS3", "JavaScript (ES6+)", "Vue.js", "Bootstrap"] },
  { category: "Backend", filter: "backend", items: ["Node.js", "Express.js", "PHP", "Python"] },
  { category: "Database", filter: "backend", items: ["MySQL"] },
  { category: "Design & Workflow", filter: "tools", items: ["Figma", "Wireframing", "Git", "GitHub"] },
];

const skillFilters = [
  { id: "all", label: "All skills" },
  { id: "frontend", label: "Frontend" },
  { id: "backend", label: "Backend & data" },
  { id: "tools", label: "Design & tools" },
];

const activeFilter = ref("all");
const visibleSkillGroups = computed(() => (
  activeFilter.value === "all"
    ? skillGroups
    : skillGroups.filter((group) => group.filter === activeFilter.value)
));

</script>

<template>
  <section id="skills" class="skills-section">
    <div class="section-heading skills-heading">
      <span class="skills-eyebrow">SKILL INVENTORY · TOOLS IN THE KIT</span>

      <h2>
        A growing
        <span>toolkit.</span>
      </h2>

      <p>
        Technologies I've used while learning, collaborating, and building
        projects — no scorecards, just tools put to work.
      </p>
    </div>

    <div class="skills-filter-tabs" role="group" aria-label="Filter skills">
      <button
        v-for="filter in skillFilters"
        :key="filter.id"
        class="filter-tab"
        :class="{ active: activeFilter === filter.id }"
        type="button"
        :aria-pressed="activeFilter === filter.id"
        @click="activeFilter = filter.id"
      >
        {{ filter.label }}
      </button>
    </div>

    <div class="skills-container">
      <article
        v-for="group in visibleSkillGroups"
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
