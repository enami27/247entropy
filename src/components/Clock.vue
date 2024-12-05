<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const currentTime = ref('');

function updateTime() {
  const now = new Date();
  currentTime.value = now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit', second: '2-digit' });
}

let timer;

onMounted(() => {
  updateTime();
  timer = setInterval(updateTime, 1000);
});

onUnmounted(() => {
  clearInterval(timer);
});
</script>

<template>
  <div class="clock">{{ currentTime }}</div>
</template>

<style scoped>
.clock {
  font-family: "VT323", monospace;
  font-size: 32px;
  color: #D8D8D8;
  text-shadow: 0px 0px 5px #D8D8D8;
  text-align: right;
  padding: 1.4vh;
}
</style>