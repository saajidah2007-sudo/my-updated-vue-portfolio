<template>
  <section id="contact" class="contact-section">
    <div class="section-heading">
      <span>CONTACT · END CREDITS</span>
      <h2>Let's connect</h2>
    </div>

    <p class="contact-intro">
      Have a project in mind, want to connect, or just want to say hello?
      Feel free to reach out.
    </p>

    <div class="contact-wrapper">
      <div class="contact-form-layout">
        <form
          action="https://formspree.io/f/xjgdrpkr"
          method="POST"
          class="contact-form"
        >
          <div class="form-group">
            <label for="name">Name</label>

            <input
              id="name"
              type="text"
              name="name"
              placeholder="Your name"
              required
            />
          </div>

          <div class="form-group">
            <label for="email">Email</label>

            <input
              id="email"
              type="email"
              name="email"
              placeholder="your@email.com"
              required
            />
          </div>

          <div class="form-group">
            <label for="message">Message</label>

            <textarea
              id="message"
              name="message"
              rows="6"
              placeholder="Tell me what's on your mind..."
              required
            ></textarea>
          </div>

          <button type="submit" class="submit-btn">
            Send Message
          </button>
        </form>

        <aside class="contact-sidekick" aria-hidden="true">
          <svg class="contact-mascot" viewBox="0 0 140 160" fill="none">
            <ellipse cx="70" cy="149" rx="38" ry="4" fill="#05090D" opacity=".35" />
            <g class="contact-mascot-tracks">
              <path d="M31 119h22c5 0 9 4 9 9v8c0 5-4 9-9 9H31c-5 0-9-4-9-9v-8c0-5 4-9 9-9Z" fill="#171E24" stroke="#68757A" stroke-width="2" />
              <path d="M87 119h22c5 0 9 4 9 9v8c0 5-4 9-9 9H87c-5 0-9-4-9-9v-8c0-5 4-9 9-9Z" fill="#171E24" stroke="#68757A" stroke-width="2" />
              <path d="M32 124v16m10-16v16m10-16v16m39-16v16m10-16v16m10-16v16" stroke="#A2AAAB" stroke-opacity=".55" stroke-width="2" />
            </g>
            <path d="M35 84c-8 1-12 7-13 14l-2 9m85-22c8 1 12 7 13 14l2 9" stroke="#68757A" stroke-width="5" stroke-linecap="round" />
            <circle cx="20" cy="110" r="4" fill="var(--accent)" />
            <circle cx="120" cy="110" r="4" fill="var(--accent)" />
            <g class="contact-mascot-body">
              <path d="M38 76c0-6 5-11 11-11h42c6 0 11 5 11 11v42H38V76Z" fill="#3A4549" stroke="var(--accent)" stroke-width="2" />
              <path d="M45 76h50v7H45z" fill="var(--accent)" opacity=".82" />
              <rect x="46" y="89" width="24" height="20" rx="3" fill="#232C31" stroke="#899194" />
              <path d="M51 95h14m-14 5h9" stroke="var(--accent)" stroke-linecap="round" stroke-width="2" />
              <circle cx="84" cy="96" r="9" fill="#232C31" stroke="#899194" stroke-width="2" />
              <circle cx="84" cy="96" r="3" fill="var(--accent)" />
              <path d="M48 117h42" stroke="var(--accent)" stroke-width="2" stroke-linecap="round" />
              <circle cx="43" cy="83" r="2" fill="#F2EEE5" />
              <circle cx="97" cy="83" r="2" fill="#F2EEE5" />
            </g>
            <g class="contact-mascot-head">
              <path d="M58 68v-8m24 8v-8" stroke="#899194" stroke-width="4" stroke-linecap="round" />
              <path d="M43 34c0-7 6-13 13-13h28c7 0 13 6 13 13v20c0 7-6 13-13 13H56c-7 0-13-6-13-13V34Z" fill="#3A4549" stroke="var(--accent)" stroke-width="2.5" />
              <path d="M49 31h42" stroke="#F2EEE5" stroke-opacity=".45" stroke-width="2" />
              <g class="contact-mascot-eyes">
                <rect x="49" y="28" width="17" height="27" rx="8.5" fill="#171E24" stroke="var(--accent)" stroke-width="2" />
                <rect x="74" y="28" width="17" height="27" rx="8.5" fill="#171E24" stroke="var(--accent)" stroke-width="2" />
                <g class="contact-mascot-pupils">
                  <circle cx="57.5" cy="42" r="5.5" fill="#899194" />
                  <circle cx="82.5" cy="42" r="5.5" fill="#899194" />
                  <circle cx="57.5" cy="42" r="2.5" fill="var(--accent)" />
                  <circle cx="82.5" cy="42" r="2.5" fill="var(--accent)" />
                </g>
                <circle cx="55.5" cy="39.5" r="1.5" fill="#F2EEE5" />
                <circle cx="80.5" cy="39.5" r="1.5" fill="#F2EEE5" />
              </g>
              <path d="M68 58h5" stroke="var(--accent)" stroke-width="2" stroke-linecap="round" />
            </g>
          </svg>
          <span class="contact-sidekick-caption">READY FOR THE NEXT SCENE</span>
        </aside>
      </div>
    </div>

    <div class="contact-info-section">
      <h3>Find me online</h3>

      <div class="contact-links">
        <a
          href="mailto:saajidah2007@gmail.com"
          class="contact-link"
        >
          <span class="contact-icon">📧</span>

          <span class="contact-text">
            <strong>Email</strong>
            <p>saajidah2007@gmail.com</p>
          </span>
        </a>

        <a
          href="https://www.linkedin.com/in/saajidah-abrahams-440178414/"
          target="_blank"
          rel="noopener noreferrer"
          class="contact-link"
        >
          <span class="contact-icon">💼</span>

          <span class="contact-text">
            <strong>LinkedIn</strong>
            <p>View My Profile</p>
          </span>
        </a>

        <a
          href="https://github.com/saajidah2007-sudo"
          target="_blank"
          rel="noopener noreferrer"
          class="contact-link"
        >
          <span class="contact-icon">💻</span>

          <span class="contact-text">
            <strong>GitHub</strong>
            <p>View My Projects</p>
          </span>
        </a>

        <div class="contact-link location">
          <span class="contact-icon">📍</span>

          <span class="contact-text">
            <strong>Location</strong>
            <p>Cape Town, South Africa</p>
          </span>
        </div>
      </div>
    </div>

    <div class="closing-credits" aria-label="Portfolio end credits">
      <div class="closing-credits-heading">
        <span>ROLL CREDITS</span>
        <span>FINAL FRAME · 01</span>
      </div>

      <dl class="closing-credit-list">
        <div>
          <dt>FEATURING</dt>
          <dd>Saajidah Abrahams</dd>
        </div>
        <div>
          <dt>ROLE</dt>
          <dd>Front-End Developer</dd>
        </div>
        <div>
          <dt>BASED IN</dt>
          <dd>Cape Town, South Africa</dd>
        </div>
        <div>
          <dt>SELECTED PROJECTS</dt>
          <dd>HRFlow · RentoSphere</dd>
        </div>
      </dl>

      <p class="closing-credits-tail">THANK YOU FOR WATCHING</p>
    </div>
  </section>
</template>