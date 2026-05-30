<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import 'bootstrap-icons/font/bootstrap-icons.css';

const dateStr = ref('');
const timeStr = ref('');
const isFullscreen = ref(false);
let timer = null;

function pad(n) { return n < 10 ? '0' + n : n; }
function getWeekday(w) {
  const arr = ['日','一','二','三','四','五','六'];
  return arr[w];
}
function updateClock() {
  const now = new Date();
  const yyyy = now.getFullYear();
  const mm = pad(now.getMonth() + 1);
  const dd = pad(now.getDate());
  const week = getWeekday(now.getDay());
  dateStr.value = `${yyyy}年${mm}月${dd}日 星期${week}`;
  const hh = pad(now.getHours());
  const min = pad(now.getMinutes());
  const ss = pad(now.getSeconds());
  timeStr.value = `${hh}:${min}:${ss}`;
}
function toggleFullScreen() {
  if (!document.fullscreenElement) {
    document.documentElement.requestFullscreen();
  } else {
    document.exitFullscreen();
  }
}
function fullscreenChange() {
  isFullscreen.value = !!document.fullscreenElement;
}
function openGithub() {
  window.open('https://github.com/1ctrl-cv/Clock-Web', '_blank');
}
onMounted(() => {
  updateClock();
  timer = setInterval(updateClock, 1000);
  document.addEventListener('fullscreenchange', fullscreenChange);
});
onBeforeUnmount(() => {
  clearInterval(timer);
  document.removeEventListener('fullscreenchange', fullscreenChange);
});
</script>

<template>
  <div class="date">{{ dateStr }}</div>
  <div class="time">{{ timeStr }}</div>
  <div id="buttons-container" v-if="!isFullscreen">
    <button class="github-btn" @click="openGithub" title="GitHub">
      <i class="bi bi-github" role="img" aria-label="GitHub"></i>
    </button>
    <button class="fullscreen-btn" @click="toggleFullScreen" title="全屏">
      <i class="bi bi-arrows-fullscreen" role="img" aria-label="Fullscreen"></i>
    </button>
  </div>
</template>

<style>
body {
  margin: 0;
  background: #000;
  color: #fff;
  font-family: 'Segoe UI', 'Arial', sans-serif;
  height: 100vh;
  overflow: hidden;
}
</style>

<style scoped>
.date, .time {
  color: oklch(84.153% .007 265.754);
}
.date {
  position: absolute;
  left: 50%;
  top: 30%;
  transform: translate(-50%, -120%);
  font-size: 4rem;
  letter-spacing: 3.4px;
}
.time {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 25rem;
  letter-spacing: 10px;
}
#buttons-container {
  position: absolute;
  top: 1.5em;
  right: 1.5em;
  display: flex;
  flex-direction: row;
  gap: 0.85em;
}
.fullscreen-btn,
.github-btn {
  position: static;
  background: none;
  color: oklch(84.153% .007 265.754);
  border: none;
  padding: 0.6rem 0.6rem;
  padding-bottom: 0.25rem;
  font-size: 1.7rem;
  border-radius: 3px;
  cursor: pointer;
  transition: background 0.17s;
}
.fullscreen-btn:hover,
.github-btn:hover {
  background: rgba(255, 255, 255, 0.15);
}

@media (min-width: 2560px) {
  .date {
    font-size: 6rem;
  }
  .time {
    font-size: 35rem;
    letter-spacing: 20px;
  }
  #buttons-container {
    top: 2em;
    right: 2em;
    gap: 1em;
  }
  .fullscreen-btn,
  .github-btn {
    font-size: 2.1rem;
    padding: 0.9rem 0.9rem;
    border-radius: 6px;
  }
}

@media (min-width: 3840px) {
  .date {
    font-size: 10rem;
  }
  .time {
    font-size: 55rem;
    letter-spacing: 30px;
  }
  #buttons-container {
    top: 3em;
    right: 3em;
    gap: 1.5em;
  }
  .fullscreen-btn,
  .github-btn {
    font-size: 3.24rem;
    padding: 1.68rem 1.68rem;
    border-radius: 12px;
  }
}
</style>
