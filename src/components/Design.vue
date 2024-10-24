<script setup>
import Modal from './Modal.vue';
import SoundEffects from './SoundEffects.vue';
import { ref } from 'vue';

defineProps({
  isVisible: {
    type: Boolean,
    required: true
  }
});

defineEmits(['close']);

const soundEffects = ref(null);

function handleEnterClick() {
  soundEffects.value.playClickSound();
}
</script>

<template>
  <Modal title="design" :isVisible="isVisible" @close="$emit('close')">
    <div class="design-content">
      <p>> mainly posters and branding work, currently learning 3d</p>
      <div class="hero">
        <img src="@/assets/blendermeme.png" alt="blender" />
        <div class="access">
          <p>design work</p>
          <div class="enter-button">
            <a 
              href="https://www.behance.net/247entropy" 
              target="_blank"
              @click="handleEnterClick"
            >ENTER</a>
          </div>
        </div>
      </div>
    </div>
  </Modal>
  <SoundEffects ref="soundEffects" />
</template>

<style scoped>
.design-content {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
  padding: 2vh;
  padding-top: 3vh;
  overflow: auto;
  flex-wrap: wrap;
  height: 100%;
}

.design-content > p {
  color: #d8d8d8;
  text-shadow: 0px 0px 2px #d8d8d8;
  font-size: 24px;
  margin-bottom: 20px;
  margin-top: 0;
}

.hero {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  flex-wrap: wrap;
}

.hero img {
  width: 50%;
  height: auto;
  object-fit: contain;
}

.access {
  display: flex;
  flex-direction: column;
  width: 50%;
  text-align: left;
  color: #d8d8d8;
  text-shadow: 0px 0px 2px #d8d8d8;
  justify-content: center;
  align-items: center;
}

.access p {
  font-size: 40px;
  margin: 0;
}

.enter-button {
  display: inline-block;
  margin-top: 10px;
  box-shadow: 0px 0px 5px #d8d8d8;
}

.enter-button a {
  display: inline-block;
  font-size: 24px;
  text-align: center;
  padding: 10px 20px;
  background-color: #d8d8d8;
  color: #101010;
  text-shadow: 0px 0px 2px #101010;
  cursor: pointer;
  text-transform: uppercase;
  text-decoration: none;  
  transition: background-color 0.3s ease;  
}

.enter-button a:hover {
  background-color: #d8d8d8;
  color: #101010; 
  box-shadow: 0px 0px 5px #d8d8d8;

  
}

@media (max-width: 1300px) {
  .hero {
    flex-direction: column;
    align-items: center;
  }

  .hero img,
  .access {
    width: 100%;
    text-align: center;
  }

  .access {
    margin-top: 5vh;
  }

  .access p {
    font-size: 30px;
  }

  .enter-button {
    width: auto;
  }
}
</style>