<script setup>
import { ref, computed } from 'vue'

const data = {
  jutsu: [
    "Kuchiose Alasan: Keyboard gue tiba-tiba kesurupan jadi Dvorak, pusing!",
    "Genjutsu Semicolon: Nyari satu titik koma doang ampe subuh, kena mental.",
    "Gak telat kok, ini lagi nunggu Gradle kelar, lama bener kek nunggu jodoh.",
    "Ketahan di Infinite Loop Tsukuyomi, gak bisa keluar-keluar nih!",
    "Jangan nanya ini jutsu apa, ini cuma kodingan gue yang lagi berantakan.",
    "Npm install-nya lebih parah dari filler Naruto, saking lamanya.",
    "Mana gue tau ini jutsu atau kodingan, yang penting jalan aja dulu lah.",
    "Lagi enak ngebenerin bug eh malah dipanggil rapat ama Lord Orochimaru.",
    "Jalan ninja gue? Push code tanpa error, itupun kalo lagi hoki.",
    "Pura-pura sibuk ngoding biar dikira beneran kerja buat Konoha.",
    "Satu bug lagi kelar nih... (bohong banget, malah nambah sepuluh).",
    "Titik koma hari ini, jadi Hokage besok pagi. Gaspol!",
    "Gausah dikomen, hapus aja langsung dengan rasa bangga!",
    "Ngoding itu kek Rasengan: butuh fokus, kopi pahit, sama mental baja."
  ]
}

const currentIdx = ref(0)
const isAnimating = ref(false)
const currentJutsuClass = ref('')

const jutsusClasses = ['anim-rasengan', 'anim-kage', 'anim-chakra']

const currentText = computed(() => data.jutsu[currentIdx.value])

const generate = () => {
  // Trigger Animation
  isAnimating.value = true
  const randomJutsu = jutsusClasses[Math.floor(Math.random() * jutsusClasses.length)]
  currentJutsuClass.value = randomJutsu
  
  setTimeout(() => {
    isAnimating.value = false
    currentJutsuClass.value = ''
  }, 1500)

  let nextIdx
  const arr = data.jutsu
  do {
    nextIdx = Math.floor(Math.random() * arr.length)
  } while (nextIdx === currentIdx.value)
  currentIdx.value = nextIdx
}
</script>

<template>
  <div class="survival-card">
    <div :class="['mascot-container', currentJutsuClass]">
      <img src="../assets/naruto.jpg" alt="Naruto" />
    </div>

    <div class="title-container">
      <h2 class="section-title">Kuchiose Alasan</h2>
    </div>

    <transition name="fade" mode="out-in">
      <div :key="currentText" class="manga-bubble">
        "{{ currentText }}"
      </div>
    </transition>
    
    <div class="controls">
      <button class="btn-primary" @click="generate">
        Keluarkan Jutsu! 🔥
      </button>
    </div>
  </div>
</template>

<style scoped>
.tabs {
  display: flex;
  gap: 15px;
  justify-content: center;
  margin-bottom: 2rem;
}
.btn-tab {
  background: var(--panel);
  color: var(--orange);
  border: 2px solid var(--orange);
  font-family: 'Bangers', cursive;
  font-size: 1.2rem;
}
.btn-tab.active {
  background: var(--orange);
  color: var(--black);
}
.manga-bubble {
  min-height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
