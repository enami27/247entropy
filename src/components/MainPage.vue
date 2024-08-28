<script setup>
import { ref, onMounted, onUnmounted} from 'vue';
import Github from './Github.vue';
import OneDayOneRender from './OneDayOneRender.vue';
import Clock from './Clock.vue';  
import Particle from './Particles.vue';  



const isGithubVisible = ref(false);
const isRenderVisible = ref(false);
const selectedIndex = ref(0);
const navItems = ref([]);

function toggleGithub() {
  isGithubVisible.value = !isGithubVisible.value;
}

function toggleRender() {
  isRenderVisible.value = !isRenderVisible.value;
}

function handleKeyDown(event) {
  if (event.key === 'ArrowUp') {
    event.preventDefault();
    selectedIndex.value = (selectedIndex.value - 1 + navItems.value.length) % navItems.value.length;
  } else if (event.key === 'ArrowDown') {
    event.preventDefault();
    selectedIndex.value = (selectedIndex.value + 1) % navItems.value.length;
  } else if (event.key === 'Enter') {
    navItems.value[selectedIndex.value].click();
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
      <div class="nav-title"><pre>           /$$                     /$$ /$$                 /$$                  /$$                               /$$
          |__/                    | $$| $$                | $$                 |__/                              | $$
  /$$$$$$  /$$ /$$   /$$  /$$$$$$ | $$| $$  /$$$$$$   /$$$$$$$       /$$    /$$ /$$  /$$$$$$$ /$$   /$$  /$$$$$$ | $$
 /$$__  $$| $$|  $$ /$$/ /$$__  $$| $$| $$ /$$__  $$ /$$__  $$      |  $$  /$$/| $$ /$$_____/| $$  | $$ |____  $$| $$
| $$  \ $$| $$ \  $$$$/ | $$$$$$$$| $$| $$| $$$$$$$$| $$  | $$       \  $$/$$/ | $$|  $$$$$$ | $$  | $$  /$$$$$$$| $$
| $$  | $$| $$  >$$  $$ | $$_____/| $$| $$| $$_____/| $$  | $$        \  $$$/  | $$ \____  $$| $$  | $$ /$$__  $$| $$
| $$$$$$$/| $$ /$$/\  $$|  $$$$$$$| $$| $$|  $$$$$$$|  $$$$$$$         \  $/   | $$ /$$$$$$$/|  $$$$$$/|  $$$$$$$| $$
| $$____/ |__/|__/  \__/ \_______/|__/|__/ \_______/ \_______/          \_/    |__/|_______/  \______/  \_______/|__/
| $$                                                                                                                 
| $$                                                                                                                 
|__/                                                                                                                 </pre></div>
      <div class="nav-links">
        <ul>
          <li :class="{ 'selected': selectedIndex === 0 }">
            <a href="https://www.behance.net/pixelledvisual" target="_blank">> design work</a>
          </li>
          <li :class="{ 'selected': selectedIndex === 1 }" @click="toggleRender">> 1day1render (in progress)</li>
          <li :class="{ 'selected': selectedIndex === 2 }">
            <a href="https://x.com/pixelledvisual" target="_blank">> x dot com</a>
          </li>
          <li :class="{ 'selected': selectedIndex === 3 }" @click="toggleGithub">> github</li>
        </ul>
      </div>
    </div>
    <Github :isVisible="isGithubVisible" @close="toggleGithub"/>
    <OneDayOneRender :isVisible="isRenderVisible" @close="toggleRender"/>
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
  color:#919DDF;
  font-family: "VT323", monospace;

}

.container * {
  text-shadow: 0px 0px 5px #919DDF;
  ;
}

.nav {
  display: flex;
  flex: 0 0 70%;
  flex-direction: column;
}

.nav-title {
  font-size: 10px;
  margin-bottom: 7vh;
}

.nav-links {
  font-size: 28px;
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
  background-color: #919DDF;
  color: #111423;
  text-decoration: underline;
}

.nav-links li.selected {
  background-color: #919DDF;
  color: #111423;
  text-decoration: underline;
}

.nav-links li.selected a {
  color: #111423;
}

li:last-child {
  margin-bottom:0vh;
}


@media (max-width:1300px) {
  .nav-title {
    font-size: 5px;
    margin-top: 4vh;
  }

}
</style>
