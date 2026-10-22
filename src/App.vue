<script setup>
import { onMounted, onUnmounted, ref } from "vue";

import "./assets/redesign.css";
import Navbar from "./components/Navbar.vue";
import Hero from "./components/Hero.vue";
import About from "./components/About.vue";
import Projects from "./components/Projects.vue";
import Skills from "./components/Skills.vue";
import Journey from "./components/Journey.vue";
import Contact from "./components/Contact.vue";
import Footer from "./components/Footer.vue";

const showBackToTop = ref(false);
let revealObserver;

const handleScroll = () => {
  showBackToTop.value = window.scrollY > 500;
};

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: "smooth",
  });
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);

  if (
    "IntersectionObserver" in window &&
    !window.matchMedia("(prefers-reduced-motion: reduce)").matches
  ) {
    document.documentElement.classList.add("reveal-ready");
    revealObserver = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add("is-visible");
            revealObserver.unobserve(entry.target);
          }
        });
      },
      { threshold: 0.12 },
    );

    document.querySelectorAll("main > section:not(.hero)").forEach((section) => {
      revealObserver.observe(section);
    });
  }
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
  revealObserver?.disconnect();
  document.documentElement.classList.remove("reveal-ready");
});
</script>

<template>
  <div class="portfolio">
    <Navbar />

    <main>
      <Hero />
      <About />
      <Projects />
      <Skills />
      <Journey />
      <Contact />
    </main>

    <Footer />

    <Transition name="fade">
      <button
        v-if="showBackToTop"
        class="back-to-top"
        @click="scrollToTop"
        aria-label="Back to top"
      >
        ↑
      </button>
    </Transition>
  </div>
</template>