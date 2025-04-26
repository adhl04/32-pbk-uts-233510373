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

    <div class="filter">
      <label>
        <input type="checkbox" v-model="showOnlyPending" />
        Tampilkan hanya yang belum selesai
      </label>
    </div>

    <ul class="activity-list">
      <li v-for="(activity, index) in filteredActivities" :key="index" class="activity-item">
        <div class="activity-content">
          <input type="checkbox" v-model="activity.done" class="checkbox" />
          <span :class="{ done: activity.done }">{{ activity.text }}</span>
        </div>
        <div class="actions">
          <button @click="removeActivity(index)" class="button-small danger">✖</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped>
:global(body) {
  font-family: 'Poppins', 'Segoe UI', sans-serif;
  width: 100%;
  height: 100dvh;
  background-image: url('/public/bcgk.jpg');
  background-size: cover;
  background-position: center;
  display: flex;
  justify-content: center;
  align-items: center;
}

.app-container {
  width: 400px;
  padding: 24px;
  background: rgba(100, 20, 20, 0.15);
  border-radius: 20px;
  box-shadow: 0px 0px 30px 20px rgb(100, 0, 100, 0.15);
  border: solid 5px rgb(225, 225, 225, 0.1);
  backdrop-filter: blur(25px);
  color: white;
  flex-direction: column;
  animation: fadeIn 1s ease;
}

.title {
  text-align: center;
  margin-bottom: 25px;
  font-size: 2.8rem;
  color: #a2a2a2;
  font-weight: 700;
}

.form {
  display: flex;
  gap: 12px;
  margin-bottom: 20px;
}

.input {
  flex: 1;
  padding: 10px 16px 10px 38px;
  border: 1px solid #ccc;
  border-radius: 99px;
  background: rgb(225, 225, 225, 0.1);
  outline: none;
  caret-color: white;
  color: white;
  font-weight: 500;
  font-size: 1rem;
  transition: all 0.3s;
}

.input::placeholder {
  color: rgb(225, 225, 225, 0.75);
}

.input:focus {
  color: white;
  border: solid 3px rgb(225, 225, 225, 0.25);
  box-shadow: 0 0 8px rgba(102, 166, 255, 0.3);
  outline: none;
}

.button {
  padding: 10px 18px;
  background-color: #707e88;
  color: white;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-size: 1rem;
  transition: background 0.3s, transform 0.2s;
}

.button:hover {
  background-color: #005fa3;
  transform: translateY(-2px);
}

.activity-list {
  list-style: none;
  padding: 0;
  margin-top: 20px;
}

.activity-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  padding: 16px 18px;
  margin-bottom: 15px;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.08);
  transition: all 0.3s ease;
  position: relative;
}

.activity-item:hover {
  transform: scale(1.02);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.15);
}

.activity-content {
  display: flex;
  align-items: center;
  gap: 12px;
}

.done {
  text-decoration: line-through;
  color: #888;
}

.checkbox {
  width: 20px;
  height: 20px;
  accent-color: #4caf50;
  cursor: pointer;
}

.activity-content span {
  font-size: 1.1rem;
  color: #333;
}

.actions {
  display: flex;
  gap: 8px;
}

.button-small {
  padding: 8px 12px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 0.9rem;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.2s;
}

.button-small:hover {
  background-color: #2980b9;
  transform: scale(1.1);
}

.danger {
  background-color: #e74c3c;
}

.danger:hover {
  background-color: #c0392b;
}

.filter {
  margin-top: 20px;
  text-align: center;
  font-size: 1rem;
  color: #dfdfdf;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-15px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
