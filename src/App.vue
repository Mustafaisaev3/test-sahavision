<template>
  <div class="app">
    <Button :variant="'secondary'" @click="openModal">Открыть</Button>
    <div v-if="selectedFolderId" class="app__selected">
      Выбранная папка: {{ selectedFolderId }}
    </div>
    <Modal
      v-if="isModalOpen"
      :title="modalTitle"
      :selected-folder-id="selectedFolderId"
      @close="closeModal"
      @select="handleSelect"
    />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import Modal from '@/components/Modal.vue';
import Button from '@/components/ui/Button.vue';

const isModalOpen = ref(false);
const modalTitle = 'Выбор папки';
const selectedFolderId = ref<number | null>(null);

const openModal = () => {
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};

const handleSelect = (folderId: number) => {
  selectedFolderId.value = folderId;
  closeModal();
};
</script>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.app__selected {
  margin-top: 20px;
  font-size: 16px;
}
</style>
