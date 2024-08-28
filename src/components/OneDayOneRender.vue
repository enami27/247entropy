<script setup>
import Modal from './Modal.vue';

defineProps({
  isVisible: {
    type: Boolean,
    required: true
  }
});

defineEmits(['close']);
</script>

<template>
  <Modal title="1day1render" :isVisible="isVisible" @close="$emit('close')">
    <div class="oneday-content">
      <p>> i'm breaking the pattern so the loop doesn't repeat tomorrow, so i'm doing 1 render a day starting aug 24th 2024.</p>
      <div class="hero">
        <img src="@/assets/blendermeme.png" alt="blender" />
        <div class="access">
          <p>1DAY1RENDER</p>
          <div>ENTER</div>
        </div>
      </div>
    </div>
  </Modal>
</template>

<style scoped>
.oneday-content {
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

.oneday-content > p {
  color: #919DDF;
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
  color: #919DDF;
  justify-content: center;
  align-items: center;
}

.access p {
  font-size: 40px;
  margin: 0;
}

.access div {
  display: inline-block;
  font-size: 24px;
  text-align: center;
  margin-top: 10px;
  padding: 10px 20px;
  background-color: #919DDF;
  color: #111423;
  cursor: pointer;
  text-transform: uppercase;
}

.access div:hover {
  background-color: #ffffff;
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

  .access div {
    width: auto;
  }
}
</style>