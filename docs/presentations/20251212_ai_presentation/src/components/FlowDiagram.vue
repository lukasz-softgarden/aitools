<script setup>
import { computed } from 'vue'

const props = defineProps({
  steps: {
    type: Array,
    required: true
  },
  direction: {
    type: String,
    default: 'horizontal',
    validator: (v) => ['horizontal', 'vertical'].includes(v)
  },
  animated: {
    type: Boolean,
    default: true
  },
  compact: {
    type: Boolean,
    default: false
  }
})

const containerClass = computed(() => ({
  'flow-diagram': true,
  'flow-horizontal': props.direction === 'horizontal',
  'flow-vertical': props.direction === 'vertical',
  'flow-compact': props.compact,
  'flow-animated': props.animated
}))
</script>

<template>
  <div :class="containerClass">
    <template v-for="(step, index) in steps" :key="index">
      <div class="flow-step-wrapper">
        <div
          class="flow-step"
          :class="{ 'flow-step-file': step.isFile }"
          :style="animated ? { animationDelay: `${index * 0.15}s` } : {}"
        >
          <div class="step-header">
            <span class="step-icon" v-if="step.icon">{{ step.icon }}</span>
            <span class="step-label">{{ step.label }}</span>
          </div>
          <span class="step-sublabel" v-if="step.sublabel">{{ step.sublabel }}</span>
        </div>
        <div v-if="step.output" class="output-section" :style="animated ? { animationDelay: `${index * 0.15 + 0.05}s` } : {}">
          <div class="output-arrow">
            <svg width="16" height="20" viewBox="0 0 16 20">
              <path d="M8 0 L8 14 M4 10 L8 14 L12 10" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </div>
          <div class="output-file">
            <span class="output-icon">{{ step.output.icon || '📄' }}</span>
            <span class="output-label">{{ step.output.label }}</span>
          </div>
        </div>
      </div>
      <div
        v-if="index < steps.length - 1"
        class="flow-arrow"
        :style="animated ? { animationDelay: `${index * 0.15 + 0.1}s` } : {}"
      >
        <svg v-if="direction === 'horizontal'" width="32" height="24" viewBox="0 0 32 24">
          <path d="M0 12 L24 12 M18 6 L24 12 L18 18" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
        <svg v-else width="24" height="32" viewBox="0 0 24 32">
          <path d="M12 0 L12 24 M6 18 L12 24 L18 18" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </div>
    </template>
  </div>
</template>

<style scoped>
.flow-diagram {
  display: flex;
  align-items: flex-start;
  gap: 0.5rem;
}

.flow-horizontal {
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-between;
  width: 100%;
}

.flow-vertical {
  flex-direction: column;
}

.flow-compact .flow-step {
  padding: 0.5rem 0.75rem;
  gap: 0.5rem;
}

.flow-compact .step-icon {
  font-size: 0.9rem;
}

.flow-compact .step-label {
  font-size: 0.85rem;
}

.flow-compact .step-sublabel {
  font-size: 0.65rem;
}

.flow-compact.flow-vertical .flow-step {
  min-width: 160px;
  justify-content: flex-start;
}

.flow-compact .flow-arrow svg {
  width: 18px;
  height: 24px;
}

.flow-step {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 0;
  padding: 0.5rem 0.75rem;
  background: white;
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
  transition: all 0.3s ease;
}

.step-header {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.4rem;
  white-space: nowrap;
  line-height: 1;
}

.flow-step-file {
  background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
  border-color: #cbd5e1;
  font-family: 'JetBrains Mono', monospace;
}

.flow-step-file .step-label {
  font-size: 0.875rem;
  color: #475569;
}

.flow-animated .flow-step {
  opacity: 0;
  transform: translateY(10px);
  animation: flowFadeIn 0.5s ease forwards;
}

.step-icon {
  font-size: 0.9rem;
}

.step-label {
  font-family: 'Outfit', sans-serif;
  font-weight: 600;
  font-size: 0.85rem;
  color: #1e293b;
  white-space: nowrap;
}

.step-sublabel {
  font-size: 0.65rem;
  color: #64748b;
  white-space: nowrap;
  margin-top: -2px;
  line-height: 1;
}

.flow-arrow {
  color: #10b981;
  flex-shrink: 0;
  display: flex;
  align-items: center;
}

.flow-compact .flow-arrow {
  height: 54px; /* Match compact step height */
}

.flow-animated .flow-arrow {
  opacity: 0;
  animation: flowFadeIn 0.3s ease forwards;
}

.flow-vertical .flow-arrow {
  transform: rotate(0deg);
}

@keyframes flowFadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Hover effect */
.flow-step:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  border-color: #10b981;
}

/* Output section styles */
.flow-step-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  align-self: flex-start;
}

.output-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 0.25rem;
}

.flow-animated .output-section {
  opacity: 0;
  animation: flowFadeIn 0.5s ease forwards;
}

.output-arrow {
  color: #94a3b8;
}

.output-file {
  display: flex;
  align-items: center;
  gap: 0.25rem;
  padding: 0.25rem 0.5rem;
  background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
  border: 1px solid #cbd5e1;
  border-radius: 6px;
  font-family: 'JetBrains Mono', monospace;
}

.output-icon {
  font-size: 0.75rem;
}

.output-label {
  font-size: 0.65rem;
  color: #475569;
}

.flow-compact .output-arrow svg {
  width: 12px;
  height: 16px;
}

.flow-compact .output-file {
  padding: 0.2rem 0.4rem;
}

.flow-compact .output-label {
  font-size: 0.6rem;
}
</style>
