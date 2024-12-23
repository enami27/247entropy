<script setup>
import { ref, onMounted, onUnmounted} from 'vue';
import Design from './Design.vue';
import Clock from './Clock.vue';  
import Particle from './Particles.vue';  
import About from './About.vue';
import SoundEffects from './SoundEffects.vue';
import { activeComponent } from './focusState';


const isDesignVisible = ref(false);
const isAboutVisible = ref(false);
const selectedIndex = ref(0);
const navItems = ref([]);
const soundEffects = ref(null);


function toggleAbout() {
  isAboutVisible.value = !isAboutVisible.value;
  soundEffects.value.playClickSound();
  activeComponent.value = isAboutVisible.value ? 'About' : 'MainPage'; // Update focus
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
  activeComponent.value = 'MainPage'; // Set focus when MainPage is mounted
  navItems.value = Array.from(document.querySelectorAll('.nav-links li'));

  const handleKeyDownForMainPage = (event) => {
    if (activeComponent.value !== 'MainPage') return; // Only handle if MainPage is active
    handleKeyDown(event);
  };

  window.addEventListener('keydown', handleKeyDownForMainPage);
  onUnmounted(() => {
    window.removeEventListener('keydown', handleKeyDownForMainPage);
  });
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
          <li :class="{ 'selected': selectedIndex === 2 }" @click="toggleAbout" @mouseover="soundEffects.playNavigationSound">> lore + links</li>
        </ul>
      </div>
      <div class="contact-email">
      <a href="mailto:247entropy@gmail.com" @mouseover="soundEffects?.playNavigationSound">247entropy@gmail.com</a> for design inquiries
    </div>
    </div>
    <Design :isVisible="isDesignVisible" @close="toggleDesign"/>
    <About :isVisible="isAboutVisible" @close="toggleAbout"/>
    <SoundEffects ref="soundEffects" />
  </div>
  
</template>

<style scoped>

.contact-email {
  position: fixed;
  bottom: 5vh;
  left: 50%;
  transform: translateX(-50%);
  font-size: 26px;
  color: #D8D8D8;
  text-shadow: 0px 0px 2px #D8D8D8;
  text-align: center;
  user-select: all;
}

.contact-email a {
  color: #D8D8D8;
  text-decoration: none;
}

.contact-email a:hover {
  background-color: #D8D8D8;
  color: #101010;
}

.clock-position {
  position: absolute;
  top: 2vh;
  right: 2vh;
  user-select: none; /* Prevent text selection */

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
  color: #D8D8D8;
  text-shadow: 0px 0px 5px #D8D8D8;
  user-select: none; /* Prevent text selection */

}

.nav-links {
  font-size: 28px;
  color: #D8D8D8;
  text-shadow: 0px 0px 2px #D8D8D8;
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
  background-color: #D8D8D8;
  color: #101010;
  text-decoration: none;
}

.nav-links li.selected {
  background-color: #D8D8D8;
  color: #101010;
  text-decoration: none;
}

.nav-links li.selected a {
  color: #101010;
}

li:last-child {
  margin-bottom:0vh;
}


@media (max-width:900px) {
  .nav-title {
    font-size: 6px;
    margin-top: 4vh;
  }

  .contact-email {
    font-size: 24px;
  }

}
</style>