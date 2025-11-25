<script setup>
import { ref, onMounted } from 'vue'

const props = defineProps({
  animated: {
    type: Boolean,
    default: true
  }
})

const isVisible = ref(false)

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 300)
})
</script>

<template>
  <div class="token-flow" :class="{ 'is-visible': isVisible }">
    <!-- Input Tokens -->
    <div class="token-group input-group">
      <div class="token-label">Tokens in</div>
      <div class="tokens">
        <div class="token" v-for="i in 4" :key="i" :style="{ animationDelay: `${i * 0.1}s` }">
          <div class="token-inner"></div>
        </div>
      </div>
    </div>

    <!-- Arrow In -->
    <div class="flow-connector">
      <svg width="60" height="24" viewBox="0 0 60 24">
        <defs>
          <linearGradient id="arrowGradient" x1="0%" y1="0%" x2="100%" y2="0%">
            <stop offset="0%" stop-color="#10b981" />
            <stop offset="100%" stop-color="#1e40af" />
          </linearGradient>
        </defs>
        <path
          d="M0 12 L48 12 M42 6 L48 12 L42 18"
          stroke="url(#arrowGradient)"
          stroke-width="2.5"
          fill="none"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="arrow-path"
        />
      </svg>
    </div>

    <!-- LLM Box -->
    <div class="llm-box">
      <div class="llm-glow"></div>
      <div class="llm-content">
        <div class="llm-icon">
          <svg width="32" height="32" viewBox="0 0 24 24" fill="none">
            <path d="M12 2L2 7L12 12L22 7L12 2Z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M2 17L12 22L22 17" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M2 12L12 17L22 12" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </div>
        <span class="llm-label">LLM</span>
      </div>
    </div>

    <!-- Arrow Out -->
    <div class="flow-connector">
      <svg width="60" height="24" viewBox="0 0 60 24">
        <path
          d="M0 12 L48 12 M42 6 L48 12 L42 18"
          stroke="url(#arrowGradient)"
          stroke-width="2.5"
          fill="none"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="arrow-path"
        />
      </svg>
    </div>

    <!-- Output Tokens -->
    <div class="token-group output-group">
      <div class="token-label">Tokens out</div>
      <div class="tokens">
        <div class="token output-token" v-for="i in 4" :key="i" :style="{ animationDelay: `${i * 0.1 + 0.8}s` }">
          <div class="token-inner"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.token-flow {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  padding: 2rem;
  opacity: 0;
  transform: scale(0.95);
  transition: all 0.6s ease;
}

.token-flow.is-visible {
  opacity: 1;
  transform: scale(1);
}

.token-group {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.75rem;
}

.token-label {
  font-family: 'Outfit', sans-serif;
  font-weight: 600;
  font-size: 1rem;
  color: #64748b;
}

.tokens {
  display: flex;
  gap: 0.5rem;
}

.token {
  width: 24px;
  height: 24px;
  border-radius: 6px;
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  opacity: 0;
  transform: translateX(-10px);
  animation: tokenIn 0.4s ease forwards;
}

.output-token {
  background: linear-gradient(135deg, #1e40af 0%, #3b82f6 100%);
  animation: tokenOut 0.4s ease forwards;
}

.token-inner {
  width: 100%;
  height: 100%;
  border-radius: 6px;
  background: rgba(255, 255, 255, 0.2);
}

.flow-connector {
  flex-shrink: 0;
}

.arrow-path {
  stroke-dasharray: 60;
  stroke-dashoffset: 60;
  animation: drawArrow 0.6s ease forwards 0.3s;
}

.llm-box {
  position: relative;
  padding: 1.5rem 2.5rem;
  background: linear-gradient(135deg, #1e293b 0%, #334155 100%);
  border-radius: 16px;
  color: white;
  box-shadow: 0 8px 32px rgba(30, 41, 59, 0.3);
}

.llm-glow {
  position: absolute;
  inset: -4px;
  border-radius: 20px;
  background: linear-gradient(135deg, #10b981, #1e40af, #10b981);
  background-size: 200% 200%;
  animation: glowPulse 3s ease infinite;
  opacity: 0.5;
  z-index: -1;
  filter: blur(8px);
}

.llm-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.llm-icon {
  color: #10b981;
}

.llm-label {
  font-family: 'Outfit', sans-serif;
  font-weight: 700;
  font-size: 1.25rem;
  letter-spacing: 0.05em;
}

@keyframes tokenIn {
  from {
    opacity: 0;
    transform: translateX(-10px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes tokenOut {
  from {
    opacity: 0;
    transform: translateX(-10px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes drawArrow {
  to {
    stroke-dashoffset: 0;
  }
}

@keyframes glowPulse {
  0%, 100% {
    background-position: 0% 50%;
    opacity: 0.5;
  }
  50% {
    background-position: 100% 50%;
    opacity: 0.7;
  }
}
</style>
