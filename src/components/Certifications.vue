<script setup>
const certifications = [
  {
    title: "Introduction to Cybersecurity",
    link: "https://drive.google.com/file/d/1otAM7wsZ2AOP82QKy2U3TmMF055-FEfw/view?usp=sharing",
    description:
      "Foundational knowledge of threat mitigation, network security, vulnerability analysis, and data protection.",
    icon: "🛡️",
  },
  {
    title: "Introduction to Data Science",
    link: "https://drive.google.com/file/d/1-Z2gJepjwT38sCV8fOH5E0c9dGHRuu7G/view?usp=sharing",
    description:
      "Foundational knowledge of data analytics, the data science lifecycle, interpretation, and visualization.",
    icon: "📈",
  },
];
</script>

<template>
  <section id="certifications" class="certifications-section" aria-labelledby="certifications-title">
    <header class="certifications-heading">
      <span class="certifications-eyebrow">ACHIEVEMENTS</span>
      <h2 id="certifications-title">Certifications</h2>
      <p>Verified learning milestones from Cisco Networking Academy.</p>
    </header>

    <div class="certification-grid">
      <article v-for="certification in certifications" :key="certification.title" class="certification-card">
        <div class="certification-card-heading">
          <div class="gym-medal" aria-hidden="true">
            <span class="gym-medal-icon">{{ certification.icon }}</span>
            <span class="gym-medal-tag">CISCO</span>
          </div>

          <div class="certification-title-group">
            <h3>{{ certification.title }}</h3>
            <p class="certification-issuer"><span aria-hidden="true">🏛️</span> Cisco Networking Academy</p>
          </div>
        </div>

        <p class="certification-description">{{ certification.description }}</p>

        <div class="certification-card-footer">
          <span class="certification-status"><span aria-hidden="true">✓</span> Cisco certification</span>
          <a :href="certification.link" target="_blank" rel="noopener noreferrer">
            View certificate <span class="certification-link-arrow" aria-hidden="true">▶</span>
          </a>
        </div>
      </article>
    </div>
  </section>
</template>
