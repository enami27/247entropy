<script setup>
import { ref } from 'vue';

const navigationSound = ref(null);
const clickSound = ref(null);
const volumeLevel = 1;

function playNavigationSound() {
  if (navigationSound.value) {
    navigationSound.value.volume = volumeLevel;
    navigationSound.value.currentTime = 0;
    navigationSound.value.play();
  }
}

function playClickSound() {
  if (clickSound.value) {
    clickSound.value.volume = volumeLevel;
    clickSound.value.currentTime = 0;
    clickSound.value.play();
  }
}

defineExpose({ playNavigationSound, playClickSound });
</script>

<template>
  <div class="hidden">
    <audio ref="navigationSound" src="@assets/navigation.mp3" preload="auto"></audio>
    <audio ref="clickSound" src="@assets/navigation.mp3" preload="auto"></audio>
  </div>
</template>