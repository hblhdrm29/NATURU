<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const emit = defineEmits(['close'])
const lines = ref([])
const errorTypes = [
  'SYSTEM: Sharingan Genjutsu Detected!',
  'FATAL ERROR: Mana depletion in chakra network',
  'Access violation: Akatsuki hack attempted',
  'CRITICAL: Hidden Leaf Barrier breach found',
  'Incompatible Jutsu: Hand signs mismatch',
  'WARNING: Itachi is watching your code...',
  'INTERNAL: Nine-Tails Chakra Leakage Detected!',
  'Error 404: Konoha Village Not Found'
]

let interval

onMounted(() => {
  interval = setInterval(() => {
    const randomError = errorTypes[Math.floor(Math.random() * errorTypes.length)]
    lines.value.push(`[${new Date().toLocaleTimeString()}] ${randomError}`)
    if (lines.value.length > 50) lines.value.shift()
    
    // Auto scroll
    const el = document.querySelector('.panic-overlay')
    if (el) el.scrollTop = el.scrollHeight
  }, 100)
})

onUnmounted(() => {
  clearInterval(interval)
})
</script>

<template>
  <div class="panic-overlay" @click="$emit('close')">
    <div class="terminal-header">=== SHARINGAN GENJUTSU VIEW ===</div>
    <div v-for="(line, i) in lines" :key="i" class="terminal-line">
      {{ line }}
    </div>
    <div class="terminal-footer">TAP TO BREAK THE GENJUTSU...</div>
  </div>
</template>

<style scoped>
.terminal-header {
  color: #fff;
  border-bottom: 2px solid var(--sharingan-red);
  margin-bottom: 1rem;
  font-weight: bold;
}
.terminal-footer {
  margin-top: 2rem;
  color: #fff;
  text-align: center;
  animation: blink 1s infinite;
  font-weight: bold;
}
@keyframes blink {
  50% { opacity: 0; }
}
</style>
