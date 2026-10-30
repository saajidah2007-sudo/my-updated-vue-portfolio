<script setup>
const journey = [
  {
    year: "2022",
    title: "Curiosity",
    text: "I became interested in technology and started wondering how websites and digital experiences are created.",
  },
  {
    year: "2025",
    title: "Discovering Life Choices",
    text: "I discovered Life Choices and found an opportunity to explore web development while working towards a career in tech.",
  },
  {
    year: "2026",
    title: "Starting My Coding Journey",
    text: "I started my internship at Life Choices and began learning the fundamentals of web development, including HTML, CSS, JavaScript, and Python.",
  },
  {
    year: "2026",
    title: "Building & Growing",
    text: "I started putting what I learned into practice through projects and began working with technologies such as Vue.js, Node.js, Express.js, and MySQL.",
  },
];
</script>

<template>
  <section id="journey" class="journey-section">

    <div class="section-heading">
      <span>TRAINER JOURNEY</span>

      <h2>
        Learning and
        <span>development</span>
      </h2>
    </div>

    <div class="timeline">

      <article
        v-for="item in journey"
        :key="`${item.year}-${item.title}`"
        class="timeline-card"
      >

        <div class="timeline-year">
          {{ item.year }}
        </div>

        <div class="timeline-dot"></div>

        <div class="timeline-content">
          <h3>
            {{ item.title }}
          </h3>

          <p>
            {{ item.text }}
          </p>
        </div>

      </article>

    </div>

  </section>
</template>
