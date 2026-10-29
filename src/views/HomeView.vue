<script setup>
import { ref } from "vue";
import About from "../components/About.vue";
import Contact from "../components/Contact.vue";
import Certifications from "../components/Certifications.vue";
import Journey from "../components/Journey.vue";
import Projects from "../components/Projects.vue";
import Skills from "../components/Skills.vue";
import heroPortrait from "../assets/hero-portrait.png";

const menuOpen = ref(false);
const formStatus = ref("idle");

const toggleMobileDrawer = () => {
  menuOpen.value = !menuOpen.value;
};

const filterAbilities = (category, event) => {
  document.querySelectorAll(".ability-tab").forEach((tab) => {
    tab.classList.remove("bg-skyBlue", "text-midnight", "border-skyBlue", "active");
    tab.classList.add("bg-panel", "border-panelBorder", "text-slate-400");
  });
  const activeButton = event.currentTarget;
  activeButton.classList.remove("bg-panel", "border-panelBorder", "text-slate-400");
  activeButton.classList.add("bg-skyBlue", "text-midnight", "border-skyBlue", "active");
  document.querySelectorAll(".ability-card").forEach((card) => {
    card.style.display = category === "all" || card.getAttribute("data-category") === category ? "flex" : "none";
  });
};

const handleTransmissionSubmit = async (event) => {
  formStatus.value = "sending";
  try {
    const response = await fetch(event.currentTarget.action, {
      method: "POST",
      body: new FormData(event.currentTarget),
      headers: { Accept: "application/json" },
    });
    if (!response.ok) throw new Error("Form submission failed");
    formStatus.value = "sent";
  } catch {
    formStatus.value = "error";
  }
};

</script>
<template>
<!-- NAVIGATION HEADER -->
    <header class="sticky top-0 z-50 bg-midnight/90 backdrop-blur-md border-b-2 border-slate-800 py-4">
        <div class="max-w-7xl mx-auto px-6 flex items-center justify-between">
            
            <!-- Brand Logo -->
            <a href="#" class="flex items-center gap-3 group">
                <div class="w-8 h-8 rounded-full bg-gradient-to-b from-red-500 to-white border-2 border-black relative flex items-center justify-center pokeball-glow">
                    <div class="w-2.5 h-2.5 bg-white border-2 border-black rounded-full"></div>
                </div>
                <span class="font-pixel text-xs sm:text-sm tracking-tight text-white group-hover:text-electricYellow transition-colors">SAAJIDAH.DEV</span>
            </a>

            <!-- Navigation Links -->
            <nav class="hidden md:flex items-center gap-8 font-semibold text-sm text-slate-400">
                <a href="#about" class="hover:text-electricYellow transition-colors">About</a>
                <a href="#skills" class="hover:text-electricYellow transition-colors">Skills</a>
                <a href="#projects" class="hover:text-electricYellow transition-colors">Projects</a>
                <a href="#journey" class="hover:text-electricYellow transition-colors">Journey</a>
                <a href="#certifications" class="hover:text-electricYellow transition-colors">Certifications</a>
                <a href="#contact" class="hover:text-electricYellow transition-colors">Contact</a>
            </nav>

            <!-- Mobile Menu Button -->
            <div class="flex items-center gap-3">
                <button id="mobile-drawer-btn" class="md:hidden text-white text-xl p-1 hover:text-electricYellow" @click="toggleMobileDrawer" :aria-expanded="menuOpen" aria-controls="mobile-drawer">
                    <i class="fa-solid fa-bars"></i>
                </button>
            </div>
        </div>

        <!-- Mobile Drawer -->
        <div id="mobile-drawer" :class="{ hidden: !menuOpen }" class="md:hidden bg-panel border-b border-panelBorder px-6 py-6 font-mono text-sm space-y-4">
            <a href="#about" class="block text-slate-300 hover:text-electricYellow mobile-nav-link" @click="menuOpen = false">01. Trainer Profile</a>
            <a href="#skills" class="block text-slate-300 hover:text-electricYellow mobile-nav-link" @click="menuOpen = false">02. Ability Index</a>
            <a href="#projects" class="block text-slate-300 hover:text-electricYellow mobile-nav-link" @click="menuOpen = false">03. Regions Explored</a>
            <a href="#journey" class="block text-slate-300 hover:text-electricYellow mobile-nav-link" @click="menuOpen = false">04. Developer Journey</a>
            <a href="#certifications" class="block text-slate-300 hover:text-electricYellow mobile-nav-link" @click="menuOpen = false">05. Badges & Credentials</a>
            <a href="#contact" class="block text-electricYellow font-bold mobile-nav-link" @click="menuOpen = false">06. Transmit Message</a>
        </div>
    </header>

    <!-- HERO SECTION (Starting Area / Pallet Town) -->
    <section id="home" class="relative py-16 md:py-28 bg-gradient-to-b from-midnight via-midnight/90 to-forest overflow-hidden border-b border-panelBorder">
        <div class="max-w-7xl mx-auto px-6 grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
            
            <!-- Dialogue & Intro -->
            <div class="lg:col-span-7 space-y-6">
                
                <!-- Pokémon Dialogue Box -->
                <div class="bg-slate-900 border-4 border-skyBlue rounded-xl p-6 shadow-2xl relative">
                    <div class="font-pixel text-xs text-electricYellow mb-3 flex items-center gap-2">
                        <span class="pokeball-icon hero-dialogue-pokeball" aria-hidden="true"></span>
                        <span>PORTFOLIO // JUNIOR WEB DEVELOPER</span>
                    </div>
                    
                    <h1 class="font-pixel text-2xl sm:text-3xl text-white leading-relaxed mb-4">
                        Hi, I’m<br>Saajidah Abrahams
                    </h1>
                    
                    <p class="font-sans font-semibold text-skyBlue text-lg mb-2">
                        Junior Web Developer &amp; UI/UX Designer
                    </p>
                    
                    <p class="text-slate-300 text-sm sm:text-base leading-relaxed">
                        I build responsive web applications with Vue, JavaScript, Node.js, and MySQL, combining full-stack development with thoughtful UI/UX design.
                    </p>

                    <!-- Triangle pointer -->
                    <div class="absolute -bottom-3 left-10 w-0 h-0 border-l-[10px] border-l-transparent border-r-[10px] border-r-transparent border-t-[12px] border-t-skyBlue"></div>
                </div>

                <!-- CTAs -->
                <div class="flex flex-wrap items-center gap-4 pt-2">
                    <a href="#projects" class="px-6 py-3.5 rounded-lg bg-electricYellow text-midnight font-pixel text-xs font-bold hover:bg-yellow-300 transition-all border-b-4 border-electricDarkYellow flex items-center gap-3 shadow-lg hover:-translate-y-0.5">
                        <i class="fa-solid fa-compass"></i>
                        <span>EXPLORE REGIONS</span>
                    </a>
                    
                    <a href="#contact" class="px-6 py-3.5 rounded-lg bg-transparent text-white border-2 border-skyBlue font-pixel text-xs hover:bg-skyBlue/10 transition-all shadow-md">
                        <i class="fa-regular fa-paper-plane mr-1"></i> GET IN TOUCH
                    </a>
                </div>

            </div>

            <!-- Trainer Card Preview -->
            <div class="lg:col-span-5 flex justify-center">
                <div class="w-full max-w-md bg-panel border-4 border-electricYellow rounded-2xl p-6 shadow-pixel-card animate-float relative">
                    
                    <div class="flex justify-between items-center mb-4 pb-2 border-b border-panelBorder font-pixel text-[10px] text-slate-400">
                        <span class="text-electricYellow">TRAINER CARD</span>
                        <span class="trainer-card-index"><span class="pokeball-icon" aria-hidden="true"></span> NO. 001</span>
                    </div>

                    <div class="w-40 h-40 mx-auto mb-5 rounded-full bg-slate-900 border-4 border-skyBlue flex items-center justify-center relative overflow-hidden shadow-blue-glow">
                        <img :src="heroPortrait" alt="Saajidah Abrahams" class="trainer-portrait">
                        <div class="absolute bottom-1 bg-electricYellow text-midnight font-pixel text-[8px] px-2 py-0.5 rounded-full font-bold">
                            LVL 2026
                        </div>
                    </div>

                    <div class="text-center space-y-2">
                        <h3 class="font-pixel text-base text-white">Saajidah Abrahams</h3>
                        <p class="font-mono text-xs text-skyBlue"><i class="fa-solid fa-compass mr-1" aria-hidden="true"></i> Cape Town, South Africa</p>
                        <div class="pt-3 border-t border-panelBorder flex justify-around font-mono text-xs text-slate-300">
                            <div>
                                <span class="block text-[10px] text-slate-500">CLASS</span>
                                <span class="font-bold text-grassGreen">Developer</span>
                            </div>
                            <div>
                                <span class="block text-[10px] text-slate-500">TRAINING</span>
                                <span class="font-bold text-electricYellow">Life Choices</span>
                            </div>
                        </div>
                    </div>

                </div>
            </div>

        </div>
        <a class="hero-next-section" href="#about" aria-label="Continue to the About section">
            <span>Continue to trainer profile</span>
            <span class="hero-next-indicator" aria-hidden="true">
                <span class="pokeball-icon hero-next-pokeball"></span>
                <span class="hero-next-arrow">▼</span>
            </span>
        </a>
    </section>

    <!-- ABOUT SECTION (Meet the Developer / Pokédex Profile) -->
    <About />

    <!-- SKILLS SECTION (Pokédex of Abilities) -->
    <Skills />

    <!-- PROJECTS SECTION (Regions Explored) -->
    <Projects />
    <Journey />
    <Certifications />

    <!-- CONTACT SECTION (Final Destination) -->
    <Contact />

    <!-- FOOTER -->
    <footer class="py-8 bg-slate-950 border-t border-panelBorder text-center font-mono text-xs text-slate-500">
        <div class="max-w-7xl mx-auto px-6 flex flex-col sm:flex-row justify-between items-center gap-4">
            <div class="flex items-center gap-2">
                <div class="w-2 h-2 rounded-full bg-electricYellow animate-ping"></div>
                <span>© 2026 SAAJIDAH ABRAHAMS // ALL RIGHTS RESERVED</span>
            </div>
        </div>
    </footer>

    <!-- INTERACTIVE SCRIPT ENGINE -->
</template>
<style>
body {
  background-color: #0c1829;
  color: #f8fafc;
  background-image: radial-gradient(rgba(255, 255, 255, 0.05) 1px, transparent 0);
  background-size: 24px 24px;
}
body::before {
  content: "";
  position: fixed;
  inset: 0;
  z-index: 99;
  pointer-events: none;
  background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.15) 50%);
  background-size: 100% 4px;
  opacity: 0.35;
}
.portfolio { overflow: visible; background: #0c1829; }
.pixel-border { border: 3px solid #334155; transition: all 0.2s ease; }
.pixel-border:hover { border-color: #facc15; }
::-webkit-scrollbar { width: 8px; height: 8px; }
::-webkit-scrollbar-track { background: #0c1829; }
::-webkit-scrollbar-thumb { background: #38bdf8; border-radius: 4px; }
::-webkit-scrollbar-thumb:hover { background: #facc15; }
@keyframes floatSlow { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-8px); } }
.animate-float { animation: floatSlow 4s ease-in-out infinite; }
@keyframes pokeballPulse { 0%, 100% { box-shadow: 0 0 10px rgba(239, 68, 68, .5); } 50% { box-shadow: 0 0 20px rgba(239, 68, 68, .9); } }
.pokeball-glow { animation: pokeballPulse 3s infinite; }
@media (prefers-reduced-motion: reduce) {
  .animate-float, .pokeball-glow { animation: none; }
  html { scroll-behavior: auto; }
}
.trainer-portrait { width: 100%; height: 100%; object-fit: cover; object-position: center; }
.trainer-card-index { display: inline-flex; align-items: center; gap: 7px; }
.trainer-card-index .pokeball-icon { width: 16px; height: 16px; flex: 0 0 16px; border-width: 1px; box-shadow: 0 0 0 1px rgba(248, 250, 252, 0.3); }
.trainer-card-index .pokeball-icon::after { width: 5px; height: 5px; border-width: 1px; }
.hero-dialogue-pokeball { width: 16px; height: 16px; flex: 0 0 16px; border-width: 1px; animation: pokeballPulse 2.5s ease-in-out infinite; }
.hero-dialogue-pokeball::after { width: 5px; height: 5px; border-width: 1px; }
.hero-next-section {
  position: absolute;
  z-index: 2;
  bottom: 18px;
  left: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 7px;
  color: #94a3b8;
  font-family: "Space Mono", monospace;
  font-size: 0.58rem;
  letter-spacing: 0.06em;
  text-decoration: none;
  text-transform: uppercase;
  transform: translateX(-50%);
  transition: color 160ms ease;
}
.hero-next-section:hover,
.hero-next-section:focus-visible { color: #facc15; }
.hero-next-section:focus-visible { outline: 2px solid #38bdf8; outline-offset: 5px; }
.hero-next-indicator { display: flex; flex-direction: column; align-items: center; gap: 3px; animation: hero-next-bounce 1.5s ease-in-out infinite; }
.hero-next-pokeball { width: 18px; height: 18px; border-width: 1px; }
.hero-next-pokeball::after { width: 5px; height: 5px; border-width: 1px; }
.hero-next-arrow { color: #38bdf8; font-family: "Press Start 2P", monospace; font-size: 0.55rem; line-height: 1; }
@keyframes hero-next-bounce { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(6px); } }
@media (prefers-reduced-motion: reduce) { .hero-next-indicator { animation: none; } }
@media (prefers-reduced-motion: reduce) { .hero-dialogue-pokeball { animation: none; } }
</style>
