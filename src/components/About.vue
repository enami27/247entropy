<script setup>
import Modal from './Modal.vue';
import SoundEffects from './SoundEffects.vue';
import { ref, onMounted, onUnmounted } from 'vue';
import { activeComponent } from './focusState';

defineProps({
  isVisible: {
    type: Boolean,
    required: true
  }
});

defineEmits(['close']);

function closeModal() {
  $emit('close');
  activeComponent.value = 'MainPage'; // Reset focus back to MainPage
}


const soundEffects = ref(null);
const selectedIndex = ref(0);
const links = ref([
  { label: 'behance', url: 'https://www.behance.net/247entropy' },
  { label: 'pinterest', url: 'https://www.pinterest.com/247entropy' },
  { label: 'x', url: 'https://x.com/247entropy' }
]);

function handleContactClick(link) {
  soundEffects.value.playClickSound();
  window.open(link.url, '_blank'); 
}

function handleKeydown(event) {
  if (event.key === 'ArrowUp') {
    event.preventDefault();
    selectedIndex.value = (selectedIndex.value - 1 + links.value.length) % links.value.length;
    soundEffects.value.playNavigationSound();
  } else if (event.key === 'ArrowDown') {
    event.preventDefault();
    selectedIndex.value = (selectedIndex.value + 1) % links.value.length;
    soundEffects.value.playNavigationSound();
  } else if (event.key === 'Enter') {
    handleContactClick(links.value[selectedIndex.value]);
  }
}


onMounted(() => {
  activeComponent.value = 'About'; // Set focus when About is opened

  const handleKeyDownForAbout = (event) => {
    if (activeComponent.value !== 'About') return; // Only handle if About is active
    handleKeydown(event);
  };

  window.addEventListener('keydown', handleKeyDownForAbout);
  onUnmounted(() => {
    window.removeEventListener('keydown', handleKeyDownForAbout);
  });
});

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown);
});
</script>


<template>
  <Modal title="lore + links" :isVisible="isVisible" @close="$emit('close')">
    <div class="about-content">
      <div class="section-content">
        <p>> freelance graphic designer, also an academiacel studying cs, math and finance</p>
        <ul class="link-list">
          <li
            v-for="(link, index) in links"
            :key="index"
            :class="{ 'selected': selectedIndex === index }"
            @click="handleContactClick(link)"
          >
            > {{ link.label }}
          </li>
        </ul>
      </div>
    </div>
  </Modal>
  <SoundEffects ref="soundEffects" />
</template>

<style scoped>
.about-content {
  padding: 2vh;
  color: #d8d8d8;
  display: flex;
  align-items: left; 
  justify-content: left;
}

.section-content {
  display: flex;
  flex-direction: column;
  align-items: left;
  justify-content: left;
  width: 100%;
  max-width: 90%;
  margin: 0 auto;
  text-align: left;
  gap: 20px;
}

.section-content p {
  font-size: 28px;
  text-shadow: 0px 0px 2px #d8d8d8;
  margin: 0;
  line-height: 1.4;
  text-align: left;
}

.link-list {
  list-style-type: none;
  padding: 0;
  margin: 20px 0 0;
  font-size: 28px;
  color: #d8d8d8;
  text-shadow: 0px 0px 2px #d8d8d8;
}

.link-list li {
  margin-bottom: 10px;
  cursor: pointer;
}

.link-list li:hover {
  background-color: #d8d8d8;
  color: #101010;
}

.link-list li.selected {
  background-color: #d8d8d8;
  color: #101010;
  text-decoration: none;
}

@media (max-width: 768px) {
  .section-content p {
    font-size: 20px;
  }
  .link-list {
    font-size: 20px;
  }
}
</style>