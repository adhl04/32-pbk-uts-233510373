<script setup>
import { ref, computed } from 'vue'
const activities = ref([])
const newActivity = ref('')

function addActivity() {
  if (newActivity.value.trim()) {
    activities.value.push({ text: newActivity.value, done: false })
    newActivity.value = ''
  }
}
</script>

<template>
  <div class="app-container">
    <h1 class="title">Daftar Kegiatan</h1>
    <form @submit.prevent="addActivity" class="form">
      <input v-model="newActivity" placeholder="Tambahkan kegiatan baru..." class="input" />
      <button type="submit" class="button">Tambah</button>
    </form>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
