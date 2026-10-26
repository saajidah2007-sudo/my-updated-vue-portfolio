<script setup>
import { ref } from "vue";

const scenes = [
  {
    title: "About Me",
    chapter: "THE INTRODUCTION",
    lead:
      "I'm an aspiring full-stack developer who enjoys turning ideas into digital experiences that are useful, intuitive, and engaging.",
    takeaway: "Curiosity is where every good build begins.",
    paragraphs: [
      "I like understanding how technology works, then combining interface design and behind-the-scenes logic to solve everyday problems.",
    ],
    tools: [],
  },
  {
    title: "What I Do",
    chapter: "DESIGNING & BUILDING",
    lead:
      "I build responsive websites and applications with HTML, CSS, JavaScript, Vue, Node.js, Express, and MySQL.",
    takeaway: "I enjoy connecting thoughtful interfaces with the logic behind them.",
    paragraphs: [
      "Projects like RentoSphere and HRFlow let me explore practical solutions, from shaping the user experience to connecting the pieces that make an app work.",
    ],
    tools: ["HTML", "CSS", "JavaScript", "Vue.js", "Node.js", "Express.js", "MySQL"],
  },
  {
    title: "Why I Do It",
    chapter: "THE CREATIVE PROCESS",
    lead:
      "What draws me to development is the combination of logic and creativity.",
    takeaway: "The best part is turning a tricky problem into something clear and useful.",
    paragraphs: [
      "I enjoy working through an idea, solving the problems along the way, and making something that feels useful, thoughtful, and easy to use.",
    ],
    tools: [],
  },
  {
    title: "What I'm Working Towards",
    chapter: "THE NEXT CHAPTER",
    lead:
      "I'm working towards becoming a well-rounded developer who can help take a project from its first idea to a finished product.",
    takeaway: "Every project is a chance to grow into a more capable developer.",
    paragraphs: [
      "I'm focused on strengthening my foundations, learning more about full-stack development, and improving how I solve problems and write maintainable code.",
    ],
    tools: [],
  },
  {
    title: "Why It Matters to Me",
    chapter: "TO BE CONTINUED",
    lead:
      "For me, development is about more than learning languages or adding projects to a portfolio.",
    takeaway: "Keep learning, keep building, one project at a time.",
    paragraphs: [
      "I'm building skills and work I can be proud of, learning from mistakes, and finding my place in the industry as I go.",
    ],
    tools: [],
  },
];

const activeScene = ref(0);
const previewScene = ref(0);
const isTransitioning = ref(false);

const goToScene = (index) => {
  previewScene.value = index;
  if (index === activeScene.value || isTransitioning.value) return;
  isTransitioning.value = true;
  activeScene.value = index;
};

const resetScenePreview = () => {
  previewScene.value = activeScene.value;
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
          I like seeing an idea
          <span>become something real.</span>
        </h3>

        <div class="about-film-card" :class="`scene-${previewScene + 1}`">
          <div class="about-film-card-top">
            <span>SAJIDAH ABRAHAMS</span>
            <span>PERSONAL REEL · 2026</span>
          </div>
          <div class="about-film-still">
            <span class="about-film-still-mark">{{ scenes[previewScene].title }}</span>
            <p class="about-film-preview-copy">{{ scenes[previewScene].lead }}</p>
            <span class="about-film-still-caption">{{ scenes[previewScene].chapter }}</span>
          </div>
          <div class="about-film-frame-nav" role="group" aria-label="Preview or open an About chapter">
            <button
              v-for="(scene, index) in scenes"
              :key="scene.title"
              class="about-film-frame"
              type="button"
              :disabled="isTransitioning"
              :aria-label="`Preview ${scene.title}: ${scene.lead}`"
              :aria-pressed="activeScene === index"
              :class="{ 'is-active': activeScene === index, 'is-preview': previewScene === index }"
              @mouseenter="previewScene = index"
              @mouseleave="resetScenePreview"
              @focus="previewScene = index"
              @blur="resetScenePreview"
              @click="goToScene(index)"
            >
              <span>{{ String(index + 1).padStart(2, "0") }}</span>
              <span class="about-film-frame-indicator" aria-hidden="true"></span>
            </button>
          </div>
          <div class="about-film-card-bottom">
            <span>PERSONAL FEATURE</span>
            <span>HOVER TO PREVIEW · SELECT TO OPEN</span>
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
              <div class="about-scene-takeaway">
                <span>THE TAKEAWAY</span>
                <p>{{ scenes[activeScene].takeaway }}</p>
              </div>
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
