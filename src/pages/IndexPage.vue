<template>
  <q-page class="landing-page row items-center justify-center">
    <div class="hero-shell column items-center text-center">
      <div class="hero-badge" :class="{ thanks: thanks }">
        <span>{{ badgeEmoji }}</span>
      </div>

      <h1 class="hero-title">{{ text }}</h1>
      <p class="hero-subtitle">{{ subtitleText }}</p>

      <div class="button-row" v-if="!thanks">
        <q-btn
          v-if="notAngryCount < 5"
          color="pink"
          glossy
          unelevated
          class="hero-btn hero-btn-primary shrink-button"
          :style="{ transform: `scale(${notAngryScale})` }"
          @click="shrinkButton"
        >
          ไม่ จะงอน 😠
        </q-btn>

        <q-btn
          color="pink"
          glossy
          unelevated
          class="hero-btn hero-btn-secondary"
          @click="showThanks"
        >
          หายงอนแล้ว
        </q-btn>
      </div>

      <div class="sent-note" v-if="thanks"></div>
      <div class="sent-note" v-else-if="notAngryCount > 0">{{ notAngryMessage }}</div>
    </div>

    <div class="hero-decorations" aria-hidden="true">
      <div class="star star-1"></div>
      <div class="star star-2"></div>
      <div class="star star-3"></div>
      <div class="bubble bubble-1"></div>
      <div class="bubble bubble-2"></div>
      <div class="bubble bubble-3"></div>
      <div class="cloud cloud-1"></div>
      <div class="cloud cloud-2"></div>
      <div class="flower-animation">
        <div class="flower flower-1"></div>
        <div class="flower flower-2"></div>
        <div class="flower flower-3"></div>
        <div class="flower flower-4"></div>
        <div class="flower flower-5"></div>
        <div class="flower flower-6"></div>
        <div class="flower flower-7"></div>
        <div class="flower flower-8"></div>
      </div>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';

const thanks = ref(false);
const notAngryScale = ref(1);
const notAngryCount = ref(0);

const badgeEmoji = computed(() => (thanks.value ? '💐' : '🥺'));
const subtitleText = computed(() =>
  thanks.value
    ? 'หายแล้วอย่างอนอีกนะ  🌸'
    : 'เปิดเข้ามาแล้ว อยากให้ง้อด้วยดอกไม้สวย ๆแบบที่แกชอบ ให้หายงอนนะ 🌸',
);
const text = computed(() =>
  thanks.value ? 'ดีใจที่แกหายงอนแล้วนะ น่ารักมากเลย  💖' : 'ขอโทษค้าบ ง้อได้มั้ยค้าบ 🥺',
);

const notAngryMessage = computed(() => {
  const messages = [
    'ไม่งอนแล้วนะ ได้มั้ยค้าบ 😊',
    'ยิ้มให้หน่อยนะ หายงอนนะ 🌼',
    'งอนไม่ลงแล้วแหละ 😅',
    'หายงอนนะคับ 😌',
    'ครั้งสุดท้ายแล้วนะ ปุ่มจะหายไปแล้ว... 🌷',
  ];
  return messages[Math.min(notAngryCount.value - 1, messages.length - 1)];
});

function shrinkButton() {
  if (notAngryCount.value >= 5) {
    return;
  }
  notAngryCount.value += 1;
  notAngryScale.value = Math.max(0.2, 1 - notAngryCount.value * 0.15);
}

function showThanks() {
  thanks.value = true;
}
</script>

<style scoped lang="scss">
.landing-page {
  min-height: 100vh;
  padding: 2.5rem 1rem;
  background: radial-gradient(circle at top, #fff5fb 0%, #ffe5f3 35%, #ffcfe2 100%);
  position: relative;
  overflow: hidden;
  font-family: 'Baloo 2', 'Comic Sans MS', cursive, sans-serif;
}

.hero-shell {
  max-width: 720px;
  width: min(92%, 560px);
  padding: 3rem 2rem;
  border-radius: 42px;
  background: rgba(255, 255, 255, 0.96);
  box-shadow: 0 30px 80px rgba(215, 95, 165, 0.18);
  backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.85);
  position: relative;
  z-index: 2;
}

.hero-badge {
  width: 136px;
  height: 136px;
  display: grid;
  place-items: center;
  margin-bottom: 1.75rem;
  border-radius: 50%;
  background: linear-gradient(135deg, #ffb8d9, #ff90c8);
  box-shadow: 0 24px 48px rgba(255, 112, 166, 0.35);
  animation: heartbeat 1.4s ease-in-out infinite;
  color: #fff;
  font-size: 4rem;
}

.hero-badge.thanks {
  background: linear-gradient(135deg, #ffdd9e, #ffb985);
  box-shadow: 0 24px 48px rgba(255, 161, 104, 0.35);
  color: #7a3b4c;
}

.hero-title {
  margin: 0;
  font-family: 'Satisfy', 'Baloo 2', cursive;
  font-size: clamp(2.4rem, 4vw, 3.6rem);
  line-height: 1.02;
  color: #6a2e5f;
  letter-spacing: -0.04em;
  text-shadow: 0 4px 12px rgba(211, 125, 164, 0.18);
  animation: floatText 5.5s ease-in-out infinite;
}

.hero-subtitle {
  margin: 1.5rem auto 1.5rem;
  max-width: 560px;
  font-family: 'Baloo 2', 'Nunito', sans-serif;
  font-size: 1.22rem;
  color: #7f5377;
  line-height: 1.85;
  letter-spacing: 0.01em;
}

.hero-message {
  display: grid;
  gap: 0.75rem;
  margin-bottom: 2rem;
  font-size: 1rem;
  color: #8a5e80;
}

.hero-message span {
  display: inline-block;
  background: rgba(255, 227, 243, 0.85);
  padding: 0.9rem 1.2rem;
  border-radius: 24px;
  border: 1px solid rgba(255, 206, 236, 0.75);
}

.button-row {
  display: flex;
  justify-content: center;
  gap: 1rem;
  flex-wrap: wrap;
  margin-top: 1.5rem;
}

.hero-btn {
  min-width: 180px;
  padding: 0.95rem 1.5rem;
  font-family: 'Baloo 2', 'Nunito', sans-serif;
  font-weight: 700;
  letter-spacing: 0.02em;
  border-radius: 999px;
  text-transform: none;
  transition:
    transform 0.25s ease,
    box-shadow 0.25s ease,
    filter 0.25s ease;
}

.hero-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 22px 48px rgba(245, 112, 179, 0.28);
}

.hero-btn:active {
  transform: translateY(0px) scale(0.98);
}

.hero-btn-primary {
  background: linear-gradient(135deg, #ff8cbc 0%, #ff60a6 52%, #ff437a 100%);
  color: #fff;
}

.hero-btn-secondary {
  background: linear-gradient(135deg, #ffe2f1 0%, #ffb5de 55%, #ff92c8 100%);
  color: #5f2b4c;
}

.shrink-button {
  transition:
    transform 0.24s ease,
    opacity 0.24s ease;
}

.sent-note {
  margin-top: 1rem;
  color: #bb4f95;
  font-size: 1rem;
  font-weight: 600;
  animation: fadeIn 0.35s ease;
}

.bubble {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.55);
  filter: blur(0.35px);
}

.bubble-1 {
  left: 20%;
  top: 24%;
  width: 22px;
  height: 22px;
  animation: bubbleDrift 10s ease-in-out infinite;
}

.bubble-2 {
  right: 28%;
  top: 22%;
  width: 18px;
  height: 18px;
  animation: bubbleDrift 12s ease-in-out infinite 1.2s;
}

.bubble-3 {
  left: 45%;
  top: 34%;
  width: 26px;
  height: 26px;
  animation: bubbleDrift 8.5s ease-in-out infinite 0.6s;
}

.flower-animation {
  position: absolute;
  inset: 0;
}

.flower {
  position: absolute;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  background: radial-gradient(
    circle at 50% 50%,
    #fff6e8 14%,
    #ffdbb2 40%,
    #ffc49c 68%,
    #ff9c86 100%
  );
  box-shadow: 0 0 20px rgba(255, 164, 187, 0.22);
}

.flower::before,
.flower::after {
  content: '';
  position: absolute;
  width: 18px;
  height: 18px;
  border-radius: 50%;
  background: radial-gradient(
    circle at 50% 50%,
    #fff6e8 20%,
    #ffd7b4 52%,
    #ffb38f 88%,
    #ff8b74 100%
  );
}

.flower::before {
  top: -10px;
  left: 50%;
  transform: translateX(-50%);
}

.flower::after {
  left: -10px;
  top: 50%;
  transform: translateY(-50%);
}

.flower-1 {
  left: 14%;
  bottom: 18%;
  width: 30px;
  height: 30px;
  animation: floatFlower 6.8s ease-in infinite;
}

.flower-2 {
  left: 66%;
  bottom: 14%;
  width: 36px;
  height: 36px;
  animation: floatFlower 8.4s ease-in infinite 1s;
}

.flower-3 {
  left: 30%;
  bottom: 6%;
  width: 32px;
  height: 32px;
  animation: floatFlower 7.6s ease-in infinite 0.4s;
}

.flower-4 {
  left: 82%;
  bottom: 28%;
  width: 24px;
  height: 24px;
  animation: floatFlower 6.2s ease-in infinite 0.8s;
}

.flower-5 {
  left: 52%;
  bottom: 3%;
  width: 40px;
  height: 40px;
  animation: floatFlower 9.4s ease-in infinite 0.2s;
}

.flower-6 {
  left: 8%;
  bottom: 24%;
  width: 22px;
  height: 22px;
  animation: floatFlower 10s ease-in infinite 0.3s;
}

.flower-7 {
  right: 18%;
  bottom: 18%;
  width: 30px;
  height: 30px;
  animation: floatFlower 7.2s ease-in infinite 0.7s;
}

.flower-8 {
  left: 40%;
  bottom: 12%;
  width: 26px;
  height: 26px;
  animation: floatFlower 11s ease-in infinite 0.5s;
}

@keyframes bubbleDrift {
  0%,
  100% {
    transform: translateY(0);
    opacity: 0.9;
  }
  50% {
    transform: translateY(-18px);
    opacity: 0.6;
  }
}

@media (max-width: 600px) {
  .landing-page {
    padding: 1.5rem 0.75rem;
  }

  .hero-shell {
    padding: 2rem 1.2rem;
    border-radius: 32px;
  }

  .hero-title {
    font-size: clamp(2rem, 9vw, 2.8rem);
  }

  .hero-subtitle {
    font-size: 1.05rem;
    line-height: 1.7;
  }

  .button-row {
    gap: 0.75rem;
  }

  .hero-btn {
    min-width: 150px;
    width: 100%;
    padding: 0.85rem 1rem;
  }

  .hero-badge {
    width: 118px;
    height: 118px;
    font-size: 3.3rem;
  }

  .flower {
    width: 22px;
    height: 22px;
  }

  .bubble-1,
  .bubble-2,
  .bubble-3 {
    width: 18px;
    height: 18px;
  }
}

.hero-decorations {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.star,
.cloud {
  position: absolute;
}

.star {
  width: 14px;
  height: 14px;
  background: radial-gradient(circle, #fff8ff 0%, #ffd6f0 65%, #ff8cc9 100%);
  border-radius: 50%;
  box-shadow: 0 0 14px rgba(255, 163, 199, 0.65);
  opacity: 0.95;
}

.star-1 {
  left: 12%;
  top: 16%;
  animation: driftStar 9s linear infinite;
}

.star-2 {
  left: 78%;
  top: 10%;
  animation: driftStar 11s linear infinite 1.1s;
}

.star-3 {
  left: 48%;
  top: 20%;
  animation: driftStar 8s linear infinite 0.6s;
}

.cloud {
  width: 140px;
  height: 90px;
  background: radial-gradient(circle at 30% 30%, #fff, #ffe3f3 55%, rgba(255, 230, 243, 0.9));
  border-radius: 70px;
  box-shadow: 0 20px 36px rgba(255, 180, 210, 0.2);
}

.cloud::before,
.cloud::after {
  content: '';
  position: absolute;
  background: inherit;
  border-radius: 50%;
}

.cloud::before {
  width: 92px;
  height: 92px;
  left: -28px;
  top: -22px;
}

.cloud::after {
  width: 84px;
  height: 84px;
  right: -26px;
  top: -12px;
}

.cloud-1 {
  left: 8%;
  top: 10%;
  transform: scale(0.82);
  animation: driftCloud 24s ease-in-out infinite;
}

.cloud-2 {
  right: 10%;
  top: 14%;
  transform: scale(0.72);
  animation: driftCloud 20s ease-in-out infinite 2s;
}

.flower-animation {
  position: absolute;
  inset: 0;
}

.flower {
  position: absolute;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  background: radial-gradient(
    circle at 50% 50%,
    #fff6e8 14%,
    #ffdbb2 40%,
    #ffc49c 68%,
    #ff9c86 100%
  );
  box-shadow: 0 0 20px rgba(255, 164, 187, 0.22);
}

.flower::before,
.flower::after {
  content: '';
  position: absolute;
  width: 18px;
  height: 18px;
  border-radius: 50%;
  background: radial-gradient(
    circle at 50% 50%,
    #fff6e8 20%,
    #ffd7b4 52%,
    #ffb38f 88%,
    #ff8b74 100%
  );
}

.flower::before {
  top: -10px;
  left: 50%;
  transform: translateX(-50%);
}

.flower::after {
  left: -10px;
  top: 50%;
  transform: translateY(-50%);
}

.flower-1 {
  left: 14%;
  bottom: 18%;
  width: 30px;
  height: 30px;
  animation: floatFlower 6.8s ease-in infinite;
}

.flower-2 {
  left: 66%;
  bottom: 14%;
  width: 36px;
  height: 36px;
  animation: floatFlower 8.4s ease-in infinite 1s;
}

.flower-3 {
  left: 30%;
  bottom: 6%;
  width: 32px;
  height: 32px;
  animation: floatFlower 7.6s ease-in infinite 0.4s;
}

.flower-4 {
  left: 82%;
  bottom: 28%;
  width: 24px;
  height: 24px;
  animation: floatFlower 6.2s ease-in infinite 0.8s;
}

.flower-5 {
  left: 52%;
  bottom: 3%;
  width: 40px;
  height: 40px;
  animation: floatFlower 9.4s ease-in infinite 0.2s;
}

.flower-6 {
  left: 8%;
  bottom: 24%;
  width: 22px;
  height: 22px;
  animation: floatFlower 10s ease-in infinite 0.3s;
}

.flower-7 {
  right: 18%;
  bottom: 18%;
  width: 30px;
  height: 30px;
  animation: floatFlower 7.2s ease-in infinite 0.7s;
}

.flower-8 {
  left: 40%;
  bottom: 12%;
  width: 26px;
  height: 26px;
  animation: floatFlower 11s ease-in infinite 0.5s;
}

@keyframes heartbeat {
  0%,
  20%,
  50%,
  80%,
  100% {
    transform: scale(1);
  }
  40% {
    transform: scale(1.14);
  }
  60% {
    transform: scale(0.98);
  }
}

@keyframes floatText {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-12px);
  }
}

@keyframes floatFlower {
  0% {
    transform: translateY(0) rotate(0deg);
    opacity: 0.92;
  }
  40% {
    transform: translateY(-60px) rotate(20deg);
    opacity: 1;
  }
  100% {
    transform: translateY(-280px) rotate(-16deg);
    opacity: 0;
  }
}

@keyframes driftStar {
  0% {
    transform: translateY(0) scale(1);
    opacity: 0.95;
  }
  50% {
    transform: translateY(-20px) scale(1.2);
  }
  100% {
    transform: translateY(8px) scale(1);
    opacity: 0.65;
  }
}

@keyframes driftCloud {
  0% {
    transform: translateX(0) scale(0.82);
  }
  50% {
    transform: translateX(16px) scale(0.84);
  }
  100% {
    transform: translateX(0) scale(0.82);
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(6px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
