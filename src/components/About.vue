<script setup>
import { ref } from "vue";

const scenes = [
  {
    title: "About Me",
    chapter: "THE INTRODUCTION",
    lead:
      "I'm an aspiring full-stack developer who enjoys turning ideas into digital experiences that are functional, intuitive, and visually engaging.",
    paragraphs: [
      "My interest in development comes from wanting to understand how technology works and how it can be used to solve problems, simplify everyday tasks, and bring creative ideas to life. I enjoy both sides of the process: designing what people see and building the logic that makes everything work behind the scenes.",
    ],
    tools: [],
  },
  {
    title: "What I Do",
    chapter: "DESIGNING & BUILDING",
    lead:
      "I build web applications and websites using technologies such as HTML, CSS, JavaScript, Vue.js, Node.js, Express.js, and MySQL.",
    paragraphs: [
      "My work involves creating responsive interfaces, developing backend functionality, working with databases, and connecting different parts of an application to create a complete experience.",
      "Through projects like RentoSphere and HRFlow, I have explored how real-world problems can be translated into practical digital solutions. I also enjoy experimenting with layouts, colours, typography, and interactions to make my work feel engaging without sacrificing usability.",
    ],
    tools: ["HTML", "CSS", "JavaScript", "Vue.js", "Node.js", "Express.js", "MySQL"],
  },
  {
    title: "Why I Do It",
    chapter: "THE CREATIVE PROCESS",
    lead:
      "What draws me to development is the combination of logic and creativity.",
    paragraphs: [
      "I like the process of starting with an idea, figuring out how it could work, and gradually building it into something tangible. There is something rewarding about solving a problem that initially seemed complicated or finally understanding why a piece of code was not working.",
      "For me, development is an opportunity to keep learning while creating things that have a purpose. I want to build technology that is not only functional but also thoughtful, accessible, and easy for people to use.",
    ],
    tools: [],
  },
  {
    title: "What I'm Working Towards",
    chapter: "THE NEXT CHAPTER",
    lead:
      "I'm working towards becoming a confident, well-rounded software developer who can contribute to projects from the initial idea through to the finished product.",
    paragraphs: [
      "I want to strengthen my technical foundations, deepen my understanding of full-stack development, and gain experience working in a professional team. I'm particularly interested in improving how I approach problem-solving, write maintainable code, and create better user experiences.",
      "Every project I take on is an opportunity to challenge myself, learn something new, and become more capable than I was before.",
    ],
    tools: [],
  },
  {
    title: "Why It Matters to Me",
    chapter: "TO BE CONTINUED",
    lead:
      "For me, this journey is about more than learning programming languages or adding projects to a portfolio.",
    paragraphs: [
      "It's about building a future through skills I can continue developing, work I can be proud of, and opportunities that allow me to grow. I know that becoming a good developer takes time, practice, and a willingness to learn from mistakes. I'm prepared to put in that work because I want to become someone who can take an idea, understand the problem behind it, and build a solution that makes a difference, no matter how small.",
      "I'm still learning, experimenting, and finding my place in the industry, but I'm excited about what lies ahead. My goal is to keep building, keep asking questions, and keep pushing myself to create better things, one project at a time.",
    ],
    tools: [],
  },
];

const activeScene = ref(0);
const isTransitioning = ref(false);

const goToScene = (index) => {
  if (index === activeScene.value || isTransitioning.value) return;
  isTransitioning.value = true;
  activeScene.value = index;
};

const showRelativeScene = (offset) => {
  const nextIndex = (activeScene.value + offset + scenes.length) % scenes.length;
  goToScene(nextIndex);
};
</script>

<template>
  <section id="about" class="about-section">
    <div class="section-heading">
      <span class="about-section-label">
        <span class="about-sticker" aria-hidden="true">✳</span>
        ABOUT ME · FIVE FRAMES
      </span>
      <h2>A story still in the making</h2>
    </div>

    <div class="about-container">
      <div class="about-intro">
        <span class="about-small-label">A personal feature · {{ scenes[activeScene].chapter }}</span>
        <h3>
          Every good story
          <span>starts somewhere.</span>
        </h3>

        <div class="about-film-card" :class="`scene-${activeScene + 1}`" aria-hidden="true">
          <div class="about-film-card-top">
            <span>SAJIDAH ABRAHAMS</span>
            <span>PERSONAL REEL · 2026</span>
          </div>
          <div class="about-film-still">
            <span class="about-film-still-mark">{{ scenes[activeScene].title }}</span>
            <span class="about-film-still-caption">{{ scenes[activeScene].chapter }}</span>
          </div>
          <div class="about-film-card-bottom">
            <span>PERSONAL FEATURE</span>
            <span>READ THIS CHAPTER</span>
          </div>
        </div>
      </div>

      <div class="about-content">
        <div class="about-scene-stage">
          <Transition
            name="about-film-slide"
            @after-enter="isTransitioning = false"
          >
            <article
              :key="activeScene"
              class="about-scene"
              aria-live="polite"
              aria-atomic="true"
            >
              <span class="about-scene-kicker">
                <span>SCENE {{ String(activeScene + 1).padStart(2, "0") }} / 05</span>
                <span class="about-scene-credit">{{ scenes[activeScene].chapter }}</span>
              </span>

              <h3>{{ scenes[activeScene].title }}</h3>
              <p class="about-lead">{{ scenes[activeScene].lead }}</p>
              <p
                v-for="paragraph in scenes[activeScene].paragraphs"
                :key="paragraph"
                class="about-scene-description"
              >
                {{ paragraph }}
              </p>

              <div v-if="scenes[activeScene].tools.length" class="about-scene-tools" aria-label="Technologies">
                <span v-for="tool in scenes[activeScene].tools" :key="tool">{{ tool }}</span>
              </div>
            </article>
          </Transition>
        </div>

        <div class="about-scene-controls">
          <button
            class="about-reel-arrow"
            type="button"
            aria-label="Previous frame"
            :disabled="isTransitioning"
            @click="showRelativeScene(-1)"
          >
            <span aria-hidden="true">←</span>
          </button>

          <div class="about-scene-nav" role="group" aria-label="Choose a story frame">
            <button
              v-for="(scene, index) in scenes"
              :key="scene.title"
              class="about-frame-button"
              type="button"
              :disabled="isTransitioning"
              :aria-label="`Show frame ${index + 1}: ${scene.title}`"
              :aria-pressed="activeScene === index"
              :class="{ 'is-active': activeScene === index }"
              @click="goToScene(index)"
            >
              <span class="about-frame-number">{{ String(index + 1).padStart(2, "0") }}</span>
              <span class="about-frame-title">{{ scene.title }}</span>
            </button>
          </div>

          <button
            class="about-reel-arrow"
            type="button"
            aria-label="Next frame"
            :disabled="isTransitioning"
            @click="showRelativeScene(1)"
          >
            <span aria-hidden="true">→</span>
          </button>
        </div>
      </div>
    </div>
  </section>
</template>
