<script setup>
import { ref, watch, onMounted, onUnmounted } from 'vue';

const props = defineProps({
  title: {
    type: String,
    default: ''
  },
  isVisible: {
    type: Boolean,
    required: true
  }
});

const emit = defineEmits(['close']);

const modalRef = ref(null);
const isDragging = ref(false);
const dragOffset = ref({ x: 0, y: 0 });
const modalStyle = ref({
  position: 'fixed',
  top: '50%',
  left: '50%',
  transform: 'translate(-50%, -50%)',
});

function handleClose() {
  emit('close');
}

function startDrag(e) {
  isDragging.value = true;
  const rect = modalRef.value.getBoundingClientRect();
  dragOffset.value = {
    x: e.clientX - rect.left,
    y: e.clientY - rect.top,
  };
  document.addEventListener('mousemove', drag);
}

function stopDrag() {
  isDragging.value = false;
  document.removeEventListener('mousemove', drag);
}

function drag(e) {
  if (!isDragging.value) return;
  const x = e.clientX - dragOffset.value.x;
  const y = e.clientY - dragOffset.value.y;
  modalStyle.value = {
    position: 'fixed',
    top: `${y}px`,
    left: `${x}px`,
    transform: 'none',
  };
}

function handleKeydown(event) {
  if (event.key === 'Escape') {
    handleClose();
  }
}

watch(() => props.isVisible, (newValue) => {
  if (newValue) {
    window.addEventListener('keydown', handleKeydown);
  } else {
    window.removeEventListener('keydown', handleKeydown);
  }
}, { immediate: true });

onMounted(() => {
  document.addEventListener('mouseup', stopDrag);
});

onUnmounted(() => {
  document.removeEventListener('mouseup', stopDrag);
  document.removeEventListener('mousemove', drag);
  window.removeEventListener('keydown', handleKeydown);
});
</script>

<template>
  <div v-if="isVisible" class="modal-container" :style="modalStyle" ref="modalRef">
    <div class="modal-bar" @mousedown="startDrag" @mouseup="stopDrag" @mouseleave="stopDrag">
      <p @click="handleClose">esc.</p>
      <p>{{ title }}</p>
    </div>
    <div class="modal-content">
      <slot></slot>
    </div>
  </div>
</template>

<style scoped>

.modal-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #101010;
  border: 2px solid #D8D8D8;
  width: 60vw; /* Increased width for larger screens */
  max-width: 900px; /* Allow more width for wide screens */
  height: 75vh;
  z-index: 10;
  box-shadow: 0px 0px 8px #D8D8D8;
  user-select: none;
  overflow: hidden;
}

.modal-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 50px;
  min-height: 50px;
  border-bottom: 2px solid #D8D8D8;
  padding: 0 2vh;
  box-sizing: border-box;
  box-shadow: 0px 0px 8px #D8D8D8;
  cursor: grab;
}

.modal-bar:active {
  cursor: grabbing;
}

.modal-bar p {
  color: #D8D8D8;
  text-shadow: 0px 0px 2px #D8D8D8;
  font-size: 24px;
  cursor:default;
  margin: 0;
  line-height: 50px;
}

.modal-content {
  flex: 1;
  width: 100%;
  height: calc(100% - 50px);
  padding: 10px;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  overflow: auto;
}

@media (max-width: 768px) {
  .modal-container {
    width: 80vw; /* Keep it wider but responsive */
  }
}

@media (max-width: 480px) {
  .modal-container {
    width: 90vw; /* Adjust width for smaller screens */
  }

  .modal-bar {
    height: 40px; /* Reduce modal bar height */
  }

  .modal-bar p {
    font-size: 18px; /* Adjust font size for better readability */
  }

  .work-title {
    font-size: 24px; /* Smaller titles for limited space */
  }

  .work-image {
    height: 200px; /* Smaller images to fit within modal */
  }
}
</style>