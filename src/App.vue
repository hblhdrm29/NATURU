<script setup>
import { ref } from 'vue'
import SurvivalCard from './components/SurvivalCard.vue'
import PanicMode from './components/PanicMode.vue'

const isPanic = ref(false)
</script>

<template>
  <PanicMode v-if="isPanic" @close="isPanic = false" />

  <header>
    <div class="header-content">
      <h1>NINJA KOK EROR</h1>
      <p class="subtitle">"ngoding pake kodok,codingan ku di obok-obok"</p>
    </div>
    <button class="btn-panic" @click="isPanic = true">GENJUTSU MODE</button>
  </header>

  <main>
    <SurvivalCard />
  </main>

  <footer>
    <p>Dibuat oleh <span>Habillah Darma</span></p>
  </footer>

</template>

<style>
header {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
}
.header-content {
  text-align: center;
}
kbd {
  background: #334155;
  padding: 2px 6px;
  border-radius: 4px;
  font-family: 'Fira Code', monospace;
  font-size: 0.8rem;
}
</style>
