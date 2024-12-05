<script setup>
import { ref } from 'vue';

const navigationSound = ref(null);
const clickSound = ref(null);

function playNavigationSound() {
  if (navigationSound.value) {
    navigationSound.value.currentTime = 0;
    navigationSound.value.play();
  }
}

function playClickSound() {
  if (clickSound.value) {
    clickSound.value.currentTime = 0;
    clickSound.value.play();
  }
}

defineExpose({ playNavigationSound, playClickSound });
</script>

<template>
  <div style="display: none;">
    <audio ref="navigationSound" preload="auto">
      <source src="@/assets/navigation.mp3" type="audio/mpeg">
    </audio>
    <audio ref="clickSound" preload="auto">
      <source src="@/assets/navigation.mp3" type="audio/mpeg">
    </audio>
  </div>
</template>