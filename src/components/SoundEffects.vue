<script setup>
import { ref } from 'vue';

// References to the audio elements
const navigationSound = ref(null);
const clickSound = ref(null);

// Volume level (0.0 to 1.0)
const volumeLevel = 0.5;

function playNavigationSound() {
  if (navigationSound.value) {
    navigationSound.value.volume = volumeLevel; // Set volume
    navigationSound.value.currentTime = 0;
    navigationSound.value.play();
  }
}

function playClickSound() {
  if (clickSound.value) {
    clickSound.value.volume = volumeLevel; // Set volume
    clickSound.value.currentTime = 0;
    clickSound.value.play();
  }
}

// Expose methods for parent component
defineExpose({ playNavigationSound, playClickSound });
</script>
