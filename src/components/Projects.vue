<script setup>
const featuredProjects = [
  {
    title: "HRFlow",
    category: "Human Resources Management System",
    description:
      "HRFlow was a group project we built for ModernTech Solutions. We created a full-stack HR system that brings different HR tasks into one place, including employee management, attendance, leave, payroll, performance, reports, and system settings.",

    image: "https://i.ibb.co/0jFNyY1b/hr-flow.png",

    technologies: ["Vue.js", "Node.js", "Express.js", "MySQL"],

    frontendGithub: "https://github.com/avivarendse/HRflow.git",
    backendGithub: "https://github.com/Zaarah-Okkers/ModernTech-Backend.git",
    live: "https://hrflow-xg3y.onrender.com/index.html",

    login: {
      username: "admin@test.com",
      password: "Test1234!",
    },
  },

  {
    title: "RentoSphere",
    category: "Rental Marketplace",
    description:
      "RentoSphere was a group project I worked on with Matthew, Lisekho, and Purrity. We built a rental marketplace where users can list items, browse products, make rental requests, and manage bookings. It also includes owner earnings dashboards, booking routes, and Nodemailer email notifications. This project gave me more experience working with Vue, Node.js, Express, and MySQL as part of a team.",

    image: "https://i.ibb.co/W4LrDP9x/Screenshot-2026-09-23-093017.png",

    technologies: ["Vue.js", "JavaScript", "Node.js", "Express.js", "MySQL"],

    github: "https://github.com/TaShepsta/E-Commerce-project.git",
    live: "https://e-commerce-project-ca0q.onrender.com",

    bookingNote: "A renter account is needed to make a booking.",
  },
];

const miniProjects = [
  {
    title: "Responsive Image Gallery",
    description:
      "One of the projects I worked on while getting more comfortable with CSS. I focused on creating a clean image layout that adjusts to different screen sizes.",

    technologies: ["HTML", "CSS"],

    image: "https://i.ibb.co/bjgDY0JY/Screenshot-2026-06-05-112231.png",

    github: "https://github.com/saajidah2007-sudo/CSS-Excercise-2.git",

    live: "https://image-gallery-css-project.netlify.app/",
  },

  {
    title: "Product Showcase Page",
    description:
      "A simple product page I built to practise working with HTML and CSS. It helped me get more comfortable with page structure, layouts, spacing, and responsive design.",

    technologies: ["HTML", "CSS"],

    image: "https://i.ibb.co/rGVWdgcH/Screenshot-2026-06-05-115837.png",

    github: "https://github.com/saajidah2007-sudo/CSS-Exercise-3.git",

    live: "https://product-showcase-css-project.netlify.app/",
  },

  {
    title: "Bootstrap Store Website",
    description:
      "A small store website I built while learning Bootstrap. I used it to practise working with Bootstrap components, cards, navigation, and responsive layouts.",

    technologies: ["HTML", "CSS", "Bootstrap"],

    image: "https://i.ibb.co/nsJkDQhr/Screenshot-2026-06-05-120132.png",

    github: "https://github.com/saajidah2007-sudo/CSS-Exercise-4.git",

    live: "https://bootstrap-store-css-project.netlify.app/",
  },
];
</script>

<template>
  <section id="projects" class="projects-section">
    <!-- SECTION INTRO -->
    <div class="section-heading projects-heading">
      <span class="section-eyebrow">MY PROJECTS</span>

      <h2>
        What I've
        <span>Worked On</span>
      </h2>

      <p>
        These are some of the projects I've worked on while learning web
        development. They include both group projects and smaller projects
        that helped me build up my skills.
      </p>
    </div>

    <div class="featured-projects">
      <article
        v-for="(project, index) in featuredProjects"
        :key="project.title"
        class="featured-project-card"
        :class="{ 'featured-project-card-reverse': index % 2 !== 0 }"
      >
        <div class="featured-project-visual">
          <div class="browser-window">
            <div class="browser-top">
              <div class="browser-dots">
                <span></span>
                <span></span>
                <span></span>
              </div>

              <div class="browser-address">
                <span>{{ project.title }} · PROJECT PREVIEW</span>
              </div>

              <div class="browser-space"></div>
            </div>

            <div class="browser-content">
              <img
                :src="project.image"
                :alt="`${project.title} project screenshot`"
                class="featured-project-screenshot"
              />
            </div>
          </div>
        </div>

        <div class="featured-project-content">
          <div class="featured-label">
            <span></span>
            Team project · Pokédex highlight
          </div>

          <div class="featured-project-title-row">
            <div>
              <p class="featured-project-category">
                {{ project.category }}
              </p>

              <h3>{{ project.title }}</h3>
            </div>
          </div>

          <p class="featured-project-description">
            {{ project.description }}
          </p>

          <div class="featured-technologies">
            <span
              v-for="technology in project.technologies"
              :key="technology"
            >
              {{ technology }}
            </span>
          </div>

          <div v-if="project.login" class="project-info-box login-box">
            <div class="info-box-heading">Demo Login</div>

            <div class="login-details">
              <div>
                <span>Username</span>
                <strong>{{ project.login.username }}</strong>
              </div>

              <div>
                <span>Password</span>
                <strong>{{ project.login.password }}</strong>
              </div>
            </div>
          </div>

          <div
            v-if="project.bookingNote"
            class="project-info-box booking-box"
          >
            <span class="booking-dot"></span>

            <p>{{ project.bookingNote }}</p>
          </div>

          <div class="featured-project-links">
            <template v-if="project.frontendGithub">
              <a
                :href="project.frontendGithub"
                target="_blank"
                rel="noopener noreferrer"
                class="project-link project-link-primary"
              >
                Frontend GitHub
              </a>

              <a
                :href="project.backendGithub"
                target="_blank"
                rel="noopener noreferrer"
                class="project-link"
              >
                Backend GitHub
              </a>
            </template>

            <template v-else>
              <a
                :href="project.github"
                target="_blank"
                rel="noopener noreferrer"
                class="project-link project-link-primary"
              >
                GitHub
              </a>
            </template>

            <a
              :href="project.live"
              target="_blank"
              rel="noopener noreferrer"
              class="project-link project-link-live"
            >
              Live Demo
            </a>
          </div>
        </div>
      </article>
    </div>

    <div class="other-projects-heading">
      <div>
        <span class="section-eyebrow">MORE POKÉDEX ENTRIES</span>

        <h3>Some Earlier Work</h3>
      </div>

      <p>
        A few smaller builds from my journey so far. Each one is a new region
        to explore and another chance to level up my skills.
      </p>
    </div>

    <div class="projects-container">
      <article
        v-for="project in miniProjects"
        :key="project.title"
        class="project-card"
      >
        <div v-if="project.image" class="project-card-image">
          <div class="mini-browser-bar">
            <span></span>
            <span></span>
            <span></span>
          </div>

          <div class="mini-project-screen">
            <img
              :src="project.image"
              :alt="`${project.title} project screenshot`"
            />
            <div class="project-art-overlay">
              <div class="project-art-tags">
                <span
                  v-for="technology in project.technologies"
                  :key="technology"
                >
                  {{ technology }}
                </span>
              </div>
            </div>
          </div>
        </div>

        <div class="project-card-content">
          <span class="project-card-type">{{ project.type || "Individual practice" }}</span>
          <h4>{{ project.title }}</h4>

          <p>
            {{ project.description }}
          </p>

          <div v-if="project.github || project.live" class="mini-project-links">
            <a
              v-if="project.github"
              :href="project.github"
              target="_blank"
              rel="noopener noreferrer"
            >
              GitHub
            </a>

            <a
              v-if="project.live"
              :href="project.live"
              target="_blank"
              rel="noopener noreferrer"
            >
              Live Demo
            </a>
          </div>
        </div>
      </article>
    </div>
  </section>
</template>
