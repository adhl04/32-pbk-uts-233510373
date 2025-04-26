<script setup>
import { ref, computed } from 'vue'
const activities = ref([])
const newActivity = ref('')
const showOnlyPending = ref(false)

function addActivity() {
  if (newActivity.value.trim()) {
    activities.value.push({ text: newActivity.value, done: false })
    newActivity.value = ''
  }
}

const filteredActivities = computed(() => {
  return showOnlyPending.value
    ? activities.value.filter(activity => !activity.done)
    : activities.value
})

function removeActivity(index) {
  activities.value.splice(index, 1)
}
</script>

<template>
  <div class="app-container">
    <h1 class="title">Daftar Kegiatan</h1>
    <form @submit.prevent="addActivity" class="form">
      <input v-model="newActivity" placeholder="Tambahkan kegiatan baru..." class="input" />
      <button type="submit" class="button">Tambah</button>
    </form>

    <ul class="activity-list">
      <li v-for="(activity, index) in filteredActivities" :key="index" class="activity-item">
        <span :class="{ done: activity.done }">{{ activity.text }}</span>
        <div class="actions">
          <button @click="removeActivity(index)" class="button-small danger">✖</button>
        </div>
      </li>
    </ul>
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
