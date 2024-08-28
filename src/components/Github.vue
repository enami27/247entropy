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
  <Modal title="github" :isVisible="isVisible" @close="$emit('close')">
    <div class="github-content">
      <img src="@/assets/maintenance.png" alt="github" />
      <p>Under maintenance for the unforeseeable future &lt/3</p>
    </div>
  </Modal>
</template>

<style scoped>
.github-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 5vh;
  height: 100%;
}

.github-content img {
  max-width: 100%;
  max-height: 50%;
  object-fit: contain;
  margin-bottom: 20px;
}

.github-content p {
  font-size: 28px;
  color: #919DDF;
  text-align: center;
  max-width: 100%;
  word-wrap: break-word;
}
</style>