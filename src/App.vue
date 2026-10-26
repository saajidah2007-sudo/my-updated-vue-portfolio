<script setup>
import { nextTick, onBeforeMount, onMounted, onUnmounted, ref } from "vue";

import "./assets/redesign.css";
import FilmLoader from "./components/FilmLoader.vue";
import Navbar from "./components/Navbar.vue";
import Hero from "./components/Hero.vue";
import About from "./components/About.vue";
import Projects from "./components/Projects.vue";
import Skills from "./components/Skills.vue";
import Journey from "./components/Journey.vue";
import Contact from "./components/Contact.vue";
import Footer from "./components/Footer.vue";

const showBackToTop = ref(false);
const isLoading = ref(true);
let revealObserver;
let isMounted = false;

onBeforeMount(() => {
  document.documentElement.classList.add("portfolio-loading");
});

const handleScroll = () => {
  showBackToTop.value = window.scrollY > 500;
};

const waitForWindowLoad = () => {
  if (document.readyState === "complete") {
    return Promise.resolve();
  }

  return new Promise((resolve) => {
    window.addEventListener("load", resolve, { once: true });
  });
};

const waitForFonts = async () => {
  if (!document.fonts?.ready) {
    return;
  }

  try {
    await document.fonts.ready;
  } catch (error) {
    console.error("Portfolio fonts could not finish loading.", error);
  }
};

const waitForImage = async (image) => {
  if (!image) {
    return;
  }

  if (!image.complete) {
    await new Promise((resolve) => {
      image.addEventListener("load", resolve, { once: true });
      image.addEventListener("error", resolve, { once: true });
    });
  }

  if (!image.naturalWidth) {
    console.error("A hero image could not be loaded.", image.currentSrc || image.src);
    return;
  }

  if (typeof image.decode === "function") {
    try {
      await image.decode();
    } catch (error) {
      console.error("A hero image could not be decoded.", error);
    }
  }
};

const waitForHeroEntrance = async () => {
  await new Promise((resolve) => {
    requestAnimationFrame(resolve);
  });

  const hero = document.querySelector(".hero");
  if (!hero) {
    return;
  }

  const animations = [...hero.querySelectorAll(".hero-info, .hero-image-wrapper")]
    .flatMap((element) => element.getAnimations())
    .filter((animation) => Number.isFinite(animation.effect?.getTiming().iterations));

  await Promise.all(
    animations.map(
      (animation) =>
        new Promise((resolve) => {
          if (animation.playState === "finished" || animation.playState === "idle") {
            resolve();
            return;
          }

          animation.addEventListener("finish", resolve, { once: true });
          animation.addEventListener("cancel", resolve, { once: true });
        }),
    ),
  );
};

const waitForPortfolioReady = async () => {
  await nextTick();

  await Promise.all([
    waitForWindowLoad(),
    waitForFonts(),
    waitForImage(document.querySelector(".hero img")),
    waitForHeroEntrance(),
  ]);

  if (isMounted) {
    isLoading.value = false;
  }
};

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: "smooth",
  });
};

onMounted(() => {
  isMounted = true;
  void waitForPortfolioReady();

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
  isMounted = false;
  window.removeEventListener("scroll", handleScroll);
  revealObserver?.disconnect();
  document.documentElement.classList.remove("reveal-ready");
  document.documentElement.classList.remove("portfolio-loading");
});

const unlockPageScroll = () => {
  document.documentElement.classList.remove("portfolio-loading");
};
</script>

<template>
  <div class="portfolio">
    <Transition name="film-loader" appear @after-leave="unlockPageScroll">
      <FilmLoader v-if="isLoading" />
    </Transition>

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