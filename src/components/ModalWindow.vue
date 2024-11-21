<template>
  <div v-if="isOpen" class="modal-overlay">
    <div class="modal">
      <header class="modal-header">
        <h3 class="title">{{ title }}</h3>
        <button @click="close">Закрыть</button>
      </header>
      <div class="modal-body">
        <slot></slot>
      </div>
      <footer class="modal-footer">
        <button @click="confirm">Ок</button>
      </footer>
    </div>
  </div>
</template>

<script setup lang="ts">
// Define props
defineProps({
  isOpen: {
    type: Boolean,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
});

// Define emits
const emit = defineEmits(["close", "confirm"]);

// Methods for emitting events
const close = () => emit("close");
const confirm = () => emit("confirm");
</script>

<style scoped>
.title {
  color: green;
}
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal {
  background: white;
  padding: 20px;
  border-radius: 8px;
  width: 400px;
}
.modal-header,
.modal-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
