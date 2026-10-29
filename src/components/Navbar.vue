<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const menuOpen = ref(false);
const activeSection = ref("home");

const sections = [
  { id: "home", label: "Home" },
  { id: "about", label: "About" },
  { id: "projects", label: "Projects" },
  { id: "skills", label: "Skills" },
  { id: "journey", label: "Journey" },
  { id: "contact", label: "Contact" },
];

const scrollToSection = (id) => {
  menuOpen.value = false;

  document.getElementById(id)?.scrollIntoView({
    behavior: window.matchMedia("(prefers-reduced-motion: reduce)").matches
      ? "auto"
      : "smooth",
  });
};

const updateActiveSection = () => {
  const scrollPosition = window.scrollY + 200;

  for (const section of sections) {
    const element = document.getElementById(section.id);

    if (
      element &&
      scrollPosition >= element.offsetTop &&
      scrollPosition < element.offsetTop + element.offsetHeight
    ) {
      activeSection.value = section.id;
      break;
    }
  }
};

onMounted(() => {
  window.addEventListener("scroll", updateActiveSection);
  updateActiveSection();
});

onUnmounted(() => {
  window.removeEventListener("scroll", updateActiveSection);
});
</script>

<template>
  <header class="site-header">
    <nav class="navbar">
      <a class="wordmark" href="#home" @click="menuOpen = false" aria-label="Saajidah Abrahams, home">
        <span class="wordmark-mark">S</span>
        <span>SAAJIDAH.DEV</span>
      </a>

      <button
        type="button"
        class="mobile-toggle"
        :class="{ open: menuOpen }"
        @click="menuOpen = !menuOpen"
        :aria-label="menuOpen ? 'Close navigation menu' : 'Open navigation menu'"
        :aria-expanded="menuOpen"
        aria-controls="primary-navigation"
      >
        <span></span>
        <span></span>
      </button>

      <ul id="primary-navigation" class="nav-links" :class="{ open: menuOpen }">
        <li v-for="section in sections" :key="section.id">
          <button
            :class="{ active: activeSection === section.id }"
            :aria-current="activeSection === section.id ? 'location' : undefined"
            @click="scrollToSection(section.id)"
          >
            {{ section.label }}
          </button>
        </li>
      </ul>
    </nav>
  </header>
</template>
