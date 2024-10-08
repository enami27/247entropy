<script setup>
import { ref, onMounted, onUnmounted} from 'vue';
import Github from './Github.vue';
import Design from './Design.vue';
import Clock from './Clock.vue';  
import Particle from './Particles.vue';  
import SoundEffects from './SoundEffects.vue';



const isGithubVisible = ref(false);
const isDesignVisible = ref(false);
const selectedIndex = ref(0);
const navItems = ref([]);
const soundEffects = ref(null);


function toggleGithub() {
  isGithubVisible.value = !isGithubVisible.value;
  soundEffects.value.playClickSound();

}

function toggleDesign() {
  isDesignVisible.value = !isDesignVisible.value;
  soundEffects.value.playClickSound();
}

function handleKeyDown(event) {
  if (event.key === 'ArrowUp') {
    event.preventDefault();
    selectedIndex.value = (selectedIndex.value - 1 + navItems.value.length) % navItems.value.length;
    soundEffects.value.playNavigationSound();
  } else if (event.key === 'ArrowDown') {
    event.preventDefault();
    selectedIndex.value = (selectedIndex.value + 1) % navItems.value.length;
    soundEffects.value.playNavigationSound();
  } else if (event.key === 'Enter') {
    navItems.value[selectedIndex.value].click();
    soundEffects.value.playClickSound();
  }
}

onMounted(() => {
  navItems.value = Array.from(document.querySelectorAll('.nav-links li'));
  window.addEventListener('keydown', handleKeyDown);
});

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeyDown);
});


</script>
<template>
  <div class="container">
    <Particle />
    <Clock class="clock-position" />
    <div class="nav">
      <div class="nav-title"><pre>
██████  ██   ██ ███████ ███████ ███    ██ ████████ ██████   ██████  ██████  ██    ██ 
     ██ ██   ██      ██ ██      ████   ██    ██    ██   ██ ██    ██ ██   ██  ██  ██  
 █████  ███████     ██  █████   ██ ██  ██    ██    ██████  ██    ██ ██████    ████   
██           ██    ██   ██      ██  ██ ██    ██    ██   ██ ██    ██ ██         ██    
███████      ██    ██   ███████ ██   ████    ██    ██   ██  ██████  ██         ██    
                                                                                     
                                                                                     
</pre></div>
      <div class="nav-links">
        <ul>
          <li :class="{ 'selected': selectedIndex === 0 }" @mouseover="soundEffects.playNavigationSound">
          </li>
          <li :class="{ 'selected': selectedIndex === 1 }" @click="toggleDesign" @mouseover="soundEffects.playNavigationSound">> design work</li>
          <li :class="{ 'selected': selectedIndex === 2 }" @mouseover="soundEffects.playNavigationSound">
            <a href="https://x.com/247entropy" target="_blank" @click="soundEffects.playClickSound">> x dot com</a>
          </li>
          <!-- <li :class="{ 'selected': selectedIndex === 3 }" @click="toggleGithub" @mouseover="soundEffects.playNavigationSound">> github</li> -->
        </ul>
      </div>
    </div>
    <Github :isVisible="isGithubVisible" @close="toggleGithub"/>
    <Design :isVisible="isDesignVisible" @close="toggleDesign"/>
    <SoundEffects ref="soundEffects" />
  </div>
</template>

<style scoped>
.clock-position {
  position: absolute;
  top: 2vh;
  right: 2vh;
}

  .container {
  position: fixed;
  top: 10vh; 
  left: 10vw;
  width: 80vw; 
  height: 80vh; 
  display: flex;
  flex-direction:row;
  justify-content: space-around;
  align-items: center;
  flex-wrap: wrap;
  overflow-y: auto;
  font-family: "VT323", monospace;

}

.nav {
  display: flex;
  flex: 0 0 70%;
  flex-direction: column;
}

.nav-title {
  font-size: 12px;
  color: #110870;
  text-shadow: 0px 0px 5px #110870;
}

.nav-links {
  font-size: 28px;
  color: #45a3ff;
  text-shadow: 0px 0px 2px #45a3ff;
}


ul {
  list-style-type: none;
  padding-left: 0;
}

li {
  margin-bottom:1.4vh ;
  cursor: pointer;

}

li a {
  text-decoration: none;
  color:inherit;
}

li:hover, li:focus {
  background-color: #45a3ff;
  color: #d7f1ff;
  text-decoration: underline;
}

.nav-links li.selected {
  background-color: #45a3ff;
  color: #d7f1ff;
  text-decoration: underline;
}

.nav-links li.selected a {
  color: #d7f1ff;
}

li:last-child {
  margin-bottom:0vh;
}


@media (max-width:1300px) {
  .nav-title {
    font-size: 6px;
    margin-top: 4vh;
  }

}
</style>
