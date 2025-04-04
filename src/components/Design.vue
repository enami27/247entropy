<script setup>
import Modal from './Modal.vue';
import SoundEffects from './SoundEffects.vue';
import { ref, onMounted, onUnmounted } from 'vue';

defineProps({
  isVisible: {
    type: Boolean,
    required: true,
  },
});

defineEmits(['close']);

const soundEffects = ref(null);
const works = ref([
{
    title: "beabadoobee",
    image: new URL('@/assets/posters/44.png', import.meta.url).href,
  },
{
    title: "gods&monsters",
    image: new URL('@/assets/posters/43.png', import.meta.url).href,
  },
{
    title: "gods&monsters",
    image: new URL('@/assets/posters/42.png', import.meta.url).href,
  },
{
    title: "newjeans",
    image: new URL('@/assets/posters/41.png', import.meta.url).href,
  },
{
    title: "newjeans",
    image: new URL('@/assets/posters/40.png', import.meta.url).href,
  },
{
    title: "distraction - kehlani",
    image: new URL('@/assets/posters/39.png', import.meta.url).href,
  },
{
    title: "i am music",
    image: new URL('@/assets/posters/38.png', import.meta.url).href,
  },
  {
    title: "yeezus",
    image: new URL('@/assets/posters/37.png', import.meta.url).href,
  },
{
    title: "General Trajectory",
    linkText: "(view full project here)",
    projectUrl: "https://www.behance.net/gallery/220512329/General-Trajectory-Visual-Identity-Logo-design",  // Replace with your actual URL
    hasLink: true,
    image: new URL('@/assets/posters/36.png', import.meta.url).href,
  },
  {
    title: "the big o",
    image: new URL('@/assets/posters/35.png', import.meta.url).href,
  },
{
    title: "alya",
    image: new URL('@/assets/posters/34.png', import.meta.url).href,
  },
{
    title: "berserk",
    image: new URL('@/assets/posters/33.png', import.meta.url).href,
  },
{
    title: "devilman crybaby",
    image: new URL('@/assets/posters/32.png', import.meta.url).href,
  },
{
    title: "misato katsuragi",
    image: new URL('@/assets/posters/31.png', import.meta.url).href,
  },
{
    title: "yoruichi (bleach)",
    image: new URL('@/assets/posters/30.png', import.meta.url).href,
  },
  {
    title: "prison school",
    image: new URL('@/assets/posters/29.png', import.meta.url).href,
  },
{
    title: "prison school",
    image: new URL('@/assets/posters/29.png', import.meta.url).href,
  },
{
    title: "levi (attack on titan)",
    image: new URL('@/assets/posters/28.png', import.meta.url).href,
  },
{
    title: "darling in the franxx",
    image: new URL('@/assets/posters/27.png', import.meta.url).href,
  },
{
    title: "baki",
    image: new URL('@/assets/posters/26.png', import.meta.url).href,
  },
{
    title: "hunter x hunter",
    image: new URL('@/assets/posters/25.png', import.meta.url).href,
  },

{
    title: "kakegurui",
    image: new URL('@/assets/posters/24.png', import.meta.url).href,
  },

  {
    title: "orebella",
    image: new URL('@/assets/posters/3.png', import.meta.url).href,
  },
  {
    title: "hurry up now",
    image: new URL('@/assets/posters/1.png', import.meta.url).href,
  },
  {
    title: "heaven knows",
    image: new URL('@/assets/posters/2.png', import.meta.url).href,
  },
  {
    title: "america's favorite dessert",
    image: new URL('@/assets/posters/5.png', import.meta.url).href,
  },
  {
    title: "gameboy color 98",
    image: new URL('@/assets/posters/6.png', import.meta.url).href,
  },
  {
    title: "naked wolfe ad",
    image: new URL('@/assets/posters/8.png', import.meta.url).href,
  },
  {
    title: "vivienne westwood",
    image: new URL('@/assets/posters/9.png', import.meta.url).href,
  },
  {
    title: "margiela 2009 glass heels",
    image: new URL('@/assets/posters/14.png', import.meta.url).href,
  },
  {
    title: "margiela replica",
    image: new URL('@/assets/posters/10.png', import.meta.url).href,
  },
  {
    title: "cdg runway",
    image: new URL('@/assets/posters/13.png', import.meta.url).href,
  },
  {
    title: "cdg parfums - mirroir by kaws",
    image: new URL('@/assets/posters/12.png', import.meta.url).href,
  },
  {
    title: "chicago aj1",
    image: new URL('@/assets/posters/17.png', import.meta.url).href,
  },
  {
    title: "blazer 77",
    image: new URL('@/assets/posters/18.png', import.meta.url).href,
  },
  {
    title: "dunks",
    image: new URL('@/assets/posters/20.png', import.meta.url).href,
  },
  {
    title: "nana osaki",
    image: new URL('@/assets/posters/16.png', import.meta.url).href,
  },
  {
    title: "neon genesis evangelion",
    image: new URL('@/assets/posters/15.png', import.meta.url).href,
  },

]);



const currentIndex = ref(0);

function prevWork() {
  soundEffects.value.playClickSound();
  currentIndex.value = (currentIndex.value - 1 + works.value.length) % works.value.length;
}

function nextWork() {
  soundEffects.value.playClickSound();
  currentIndex.value = (currentIndex.value + 1) % works.value.length;
}

function handleKeydown(event) {
  if (event.key === 'ArrowLeft') {
    prevWork();
  } else if (event.key === 'ArrowRight') {
    nextWork();
  }
}

onMounted(() => {
  window.addEventListener('keydown', handleKeydown);

  // Preload all images
  works.value.forEach(work => {
    const img = new Image();
    img.src = work.image;
  });
});

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown);
});
</script>

<template>
  <Modal title="design" :isVisible="isVisible" @close="$emit('close')">
    <div class="design-showcase">
      <div class="arrow left" @click="prevWork"><span>&lt;</span></div>
      <div class="work-content">
        <div class="title-container">
          <h2 class="work-title">{{ works[currentIndex].title }}</h2>
          <a v-if="works[currentIndex].hasLink" 
             :href="works[currentIndex].projectUrl" 
             target="_blank" 
             rel="noopener noreferrer"
             class="project-link">
            {{ works[currentIndex].linkText }}
          </a>
        </div>
        <img :src="works[currentIndex].image" alt="Design Work" class="work-image" />
      </div>
      <div class="arrow right" @click="nextWork"><span>&gt;</span></div>
    </div>
  </Modal>
  <SoundEffects ref="soundEffects" />
</template>


<style scoped>
.title-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}

.work-title {
  font-size: 32px;
  color: #d8d8d8;
  text-shadow: 0px 0px 2px #d8d8d8;
  margin-bottom: 8px;
  text-align: center;
}

.project-link {
  font-size: 20px;
  color: #a8d8ff;
  text-decoration: underline;
  cursor: pointer;
  transition: color 0.2s;
}

.project-link:hover {
  color: #ffffff;
  text-shadow: 0px 0px 4px #a8d8ff;
}

.design-showcase {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
  position: relative;
}

.arrow {
  cursor: pointer;
  font-size: 36px;
  color: #d8d8d8;
  user-select: none;
  width: 50px;
  text-align: center;
  line-height: 100%;
}

.arrow.left {
  margin-left: 10px;
}

.arrow.right {
  margin-right: 10px;
}

.work-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
}
.work-image {
  height: 350px;  /* Fixed height */
  width: auto;    /* Maintain aspect ratio */
  max-width: 100%;  /* Ensure it fits within container */
  object-fit: contain;  /* Preserve image proportions */
  margin: 10px 0;
  box-shadow: 0px 0px 8px #d8d8d8;
}
.tools {
  margin-top: 20px;
}
</style>