<template>
  <div class="film-loader-screen" role="status" aria-label="Loading portfolio">
    <div class="film-loader-content">
      <div class="camera" aria-hidden="true">
        <span class="camera-viewfinder"></span>
        <span class="camera-record-light"></span>
        <span class="camera-lens">
          <span class="camera-aperture"></span>
        </span>
      </div>

      <p class="loader-eyebrow">SAAJIDAH ABRAHAMS · PORTFOLIO</p>
      <h1>Rolling into the scene<span>.</span></h1>
      <p class="loader-caption">A little patience. The picture is developing.</p>

      <div
        class="loader-progress"
        role="progressbar"
        aria-label="Loading portfolio"
        aria-valuemin="0"
        aria-valuemax="100"
      >
        <span></span>
      </div>
      <p class="loader-status">PLEASE STAND BY</p>
    </div>
  </div>
</template>

<style scoped>
.film-loader-screen {
  position: fixed;
  z-index: 40;
  inset: 0;
  display: grid;
  place-items: center;
  overflow: hidden;
  padding: 24px;
  background:
    radial-gradient(ellipse at 50% 42%, rgba(225, 182, 109, 0.1), transparent 42%),
    #111820;
  color: #f2eee5;
  text-align: center;
}

.film-loader-screen::before,
.film-loader-screen::after {
  position: absolute;
  inset: 18px;
  border: 1px solid rgba(225, 182, 109, 0.17);
  content: "";
  pointer-events: none;
}

.film-loader-screen::after {
  inset: 26px;
  border-color: rgba(242, 238, 229, 0.06);
}

.film-loader-content {
  position: relative;
  z-index: 1;
  width: min(100%, 460px);
}

.camera {
  position: relative;
  width: 112px;
  height: 77px;
  margin: 0 auto 38px;
  border: 1px solid rgba(242, 238, 229, 0.76);
  border-radius: 9px;
  background: linear-gradient(145deg, #35414a, #202a32 68%);
  box-shadow:
    0 18px 38px rgba(0, 0, 0, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.16);
  animation: camera-arrive 600ms ease-out both;
}

.camera::before {
  position: absolute;
  top: -11px;
  left: 18px;
  width: 36px;
  height: 11px;
  border: 1px solid rgba(242, 238, 229, 0.76);
  border-bottom: 0;
  border-radius: 5px 5px 0 0;
  background: #2d3942;
  content: "";
}

.camera-viewfinder {
  position: absolute;
  top: 12px;
  left: 16px;
  width: 20px;
  height: 13px;
  border: 1px solid rgba(225, 182, 109, 0.8);
  border-radius: 2px;
  background: rgba(225, 182, 109, 0.12);
}

.camera-record-light {
  position: absolute;
  top: 17px;
  right: 14px;
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: #e56a56;
  box-shadow: 0 0 12px rgba(229, 106, 86, 0.8);
  animation: record-pulse 1.2s ease-in-out infinite;
}

.camera-lens {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 49px;
  height: 49px;
  display: grid;
  place-items: center;
  border: 2px solid #e1b66d;
  border-radius: 50%;
  background: #151c22;
  box-shadow:
    0 0 0 4px #29343c,
    0 0 0 5px rgba(242, 238, 229, 0.56),
    0 0 23px rgba(225, 182, 109, 0.28);
  transform: translate(-50%, -50%);
}

.camera-aperture {
  width: 27px;
  height: 27px;
  border: 1px solid rgba(225, 182, 109, 0.8);
  border-radius: 50%;
  background:
    radial-gradient(circle, #111820 0 25%, transparent 27%),
    conic-gradient(
      from 20deg,
      #d6aa60 0 12%,
      #26333b 12% 25%,
      #d6aa60 25% 37%,
      #26333b 37% 50%,
      #d6aa60 50% 62%,
      #26333b 62% 75%,
      #d6aa60 75% 87%,
      #26333b 87%
    );
}

.loader-eyebrow,
.loader-status {
  color: #e1b66d;
  font-size: 0.66rem;
  font-weight: 700;
  letter-spacing: 0.18em;
  text-transform: uppercase;
}

.loader-eyebrow {
  margin: 0 0 12px;
}

.film-loader-content h1 {
  margin: 0;
  font-size: clamp(1.8rem, 7vw, 3rem);
  font-weight: 700;
  letter-spacing: -0.06em;
  line-height: 1.1;
}

.film-loader-content h1 span {
  color: #e1b66d;
}

.loader-caption {
  margin: 13px 0 27px;
  color: #b3b9bb;
  font-size: 0.9rem;
}

.loader-progress {
  width: min(100%, 260px);
  height: 2px;
  margin: 0 auto 13px;
  overflow: hidden;
  background: rgba(242, 238, 229, 0.18);
}

.loader-progress span {
  width: 100%;
  height: 100%;
  display: block;
  background: #e1b66d;
  transform: scaleX(0);
  transform-origin: left;
  animation: load-film 400ms 60ms ease-in-out forwards;
}

.loader-status {
  margin: 0;
  color: #a3a9ad;
  font-size: 0.56rem;
}

.film-loader-enter-active,
.film-loader-leave-active {
  transition: opacity 280ms ease, visibility 280ms ease;
}

.film-loader-enter-from,
.film-loader-leave-to {
  opacity: 0;
  visibility: hidden;
}

@keyframes camera-arrive {
  from {
    opacity: 0;
    transform: translateY(10px) scale(0.94);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@keyframes record-pulse {
  50% {
    opacity: 0.45;
  }
}

@keyframes load-film {
  to {
    transform: scaleX(1);
  }
}

@media (prefers-reduced-motion: reduce) {
  .camera,
  .camera-record-light,
  .loader-progress span {
    animation: none;
  }

  .loader-progress span {
    transform: scaleX(1);
  }

  .film-loader-enter-active,
  .film-loader-leave-active {
    transition-duration: 100ms;
  }
}
</style>
