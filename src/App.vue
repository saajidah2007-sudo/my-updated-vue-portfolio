<script setup>
import { onMounted, onUnmounted, ref } from "vue";

import "./assets/redesign.css";
import "./assets/pixel-theme.css";

const showBackToTop = ref(false);
const isTeleporting = ref(false);
let teleportTimer;

const handleScroll = () => {
  showBackToTop.value = window.scrollY > 500;
};

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: window.matchMedia("(prefers-reduced-motion: reduce)").matches
      ? "auto"
      : "smooth",
  });
};

const teleportToTop = () => {
  if (isTeleporting.value) return;

  isTeleporting.value = true;
  const teleportDuration = window.matchMedia("(prefers-reduced-motion: reduce)").matches
    ? 0
    : 420;
  teleportTimer = window.setTimeout(() => {
    scrollToTop();
    isTeleporting.value = false;
  }, teleportDuration);
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
  window.clearTimeout(teleportTimer);
});
</script>

<template>
  <div class="portfolio">
    <RouterView />

    <Transition name="fade">
      <button
        v-if="showBackToTop"
        class="back-to-top"
        :class="{ teleporting: isTeleporting }"
        @click="teleportToTop"
        :disabled="isTeleporting"
        aria-label="Teleport Abra to the top"
        title="Teleport Abra to the top"
      >
        <span class="teleport-portal" aria-hidden="true"></span>
        <span class="teleport-pokemon" aria-hidden="true"><svg viewBox="0 0 64 64" role="img" focusable="false"><path d="M45 42 56 46 51 51 58 54 55 59 43 53Z" fill="#d49b32"/><path d="M11 22 8 4 23 17 27 23M38 18 54 4 52 24 43 27" fill="#e8b746" stroke="#9b6729" stroke-width="2"/><path d="m12 9 8 9-7 1ZM49 10l-8 8 9 2Z" fill="#81502d"/><path d="M19 19 24 15 40 15 46 20 45 34 40 39 23 37 18 31Z" fill="#f2c75c" stroke="#9b6729" stroke-width="1.5"/><path d="M22 26h6v2h-6m13 0h6v-2h-6" fill="#573b31"/><path d="M29 31h5v2h-5" fill="#9b6729"/><path d="m19 36-7 5 2 4 11-4m20-5 7 5-2 4-11-4" fill="#e8b746" stroke="#9b6729" stroke-width="1.5"/><path d="m24 37 16 1 4 11-8 4h-9l-8-5Z" fill="#e8b746" stroke="#9b6729" stroke-width="1.5"/><path d="m23 40 5 1 2 7-6-1m14-6 4-1-1 7-5 1Z" fill="#81502d"/><path d="m25 51 8 1-1 7H20v-3Zm9 1 8-2 5 6-2 3H34Z" fill="#e8b746" stroke="#9b6729" stroke-width="1.5"/></svg></span>
        <span class="teleport-spark" aria-hidden="true">✦</span>
        ↑
      </button>
    </Transition>
  </div>
</template>
