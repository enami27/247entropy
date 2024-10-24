<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const canvas = ref(null);

const particles = [];
const particleCount = 200;
const particleColor = '#D8D8D8';
const particleSize = 2;
const particleSpeed = 0.7;

function createParticles() {
  for (let i = 0; i < particleCount; i++) {
    particles.push({
      x: Math.random() * canvas.value.width,
      y: Math.random() * canvas.value.height,
      speedX: (Math.random() - 0.5) * particleSpeed,
      speedY: (Math.random() - 0.5) * particleSpeed
    });
  }
}

function updateParticles() {
  particles.forEach(particle => {
    particle.x += particle.speedX;
    particle.y += particle.speedY;

    if (particle.x < 0 || particle.x > canvas.value.width) particle.speedX *= -1;
    if (particle.y < 0 || particle.y > canvas.value.height) particle.speedY *= -1;
  });
}

function drawParticles(ctx) {
  ctx.clearRect(0, 0, canvas.value.width, canvas.value.height);
  ctx.fillStyle = particleColor;

  particles.forEach(particle => {
    ctx.beginPath();
    ctx.arc(particle.x, particle.y, particleSize, 0, Math.PI * 2);
    ctx.fill();
  });
}

function animate() {
  if (!canvas.value) return;
  const ctx = canvas.value.getContext('2d');
  updateParticles();
  drawParticles(ctx);
  requestAnimationFrame(animate);
}

function handleResize() {
  if (canvas.value) {
    canvas.value.width = window.innerWidth;
    canvas.value.height = window.innerHeight;
  }
}

onMounted(() => {
  handleResize();
  createParticles();
  animate();
  window.addEventListener('resize', handleResize);
});

onUnmounted(() => {
  window.removeEventListener('resize', handleResize);
});
</script>

<template>
  <canvas ref="canvas" class="particle-canvas"></canvas>
</template>

<style scoped>
.particle-canvas {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  opacity: 0.5;
}
</style>