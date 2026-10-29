<script setup>
import { onMounted, onUnmounted, ref } from "vue";

import "./assets/redesign.css";
import "./assets/pixel-theme.css";

const showBackToTop = ref(false);
const isTeleporting = ref(false);
const showIntro = ref(true);
const introCharging = ref(true);
const introOpening = ref(false);
const introFlash = ref(false);
let teleportTimer;
let introStartTimer;
let introFlashTimer;
let introCloseTimer;

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

const finishIntro = () => {
  showIntro.value = false;
  document.documentElement.scrollTop = 0;
  document.body.scrollTop = 0;
  document.documentElement.classList.remove("portfolio-loading");
  document.documentElement.classList.add("opening-complete");
};

const openIntro = () => {
  if (!showIntro.value || introOpening.value) return;
  window.clearTimeout(introStartTimer);
  introCharging.value = false;
  introOpening.value = true;
  introFlashTimer = window.setTimeout(() => { introFlash.value = true; }, 100);
  introCloseTimer = window.setTimeout(finishIntro, 850);
};

const skipIntro = () => {
  window.clearTimeout(introStartTimer);
  window.clearTimeout(introFlashTimer);
  window.clearTimeout(introCloseTimer);
  finishIntro();
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
  if (window.matchMedia("(prefers-reduced-motion: reduce)").matches) {
    skipIntro();
  } else {
    document.documentElement.classList.add("portfolio-loading");
    introStartTimer = window.setTimeout(openIntro, 1100);
  }
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
  window.clearTimeout(teleportTimer);
  window.clearTimeout(introStartTimer);
  window.clearTimeout(introFlashTimer);
  window.clearTimeout(introCloseTimer);
  document.documentElement.classList.remove("portfolio-loading");
});
</script>

<template>
  <div class="portfolio">
    <Transition name="pokeball-intro">
      <div
        v-if="showIntro"
        id="pokeball-intro-overlay"
        :class="{
          'pokeball-charging': introCharging,
          'pokeball-open': introOpening,
        }"
        role="dialog"
        aria-label="Poké Ball page intro"
        aria-modal="true"
      >
        <div class="pokeball-shell pokeball-top" aria-hidden="true"></div>
        <div class="pokeball-shell pokeball-bottom" aria-hidden="true"></div>
        <div class="flash-reveal-overlay" :class="{ 'flash-active': introFlash }" aria-hidden="true"></div>
        <button class="pokeball-center-btn" type="button" @click="openIntro" aria-label="Open the Poké Ball intro">
          <span class="pokeball-inner-dot"></span>
        </button>
        <p class="pokeball-status-text" aria-live="polite">{{ introOpening ? "Welcome, Trainer!" : "Loading your adventure..." }}</p>
        <button class="skip-intro-btn" type="button" @click="skipIntro">Skip intro</button>
      </div>
    </Transition>

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
