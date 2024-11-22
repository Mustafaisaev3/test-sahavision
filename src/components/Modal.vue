<template>
  <div class="modal">
    <div class="modal__overlay" @click="closeModal"></div>
    <div class="modal__content">
      <div class="modal__header">
        <h2 class="modal__title">{{ title }}</h2>
        <span class="modal__close-button" @click="closeModal">
          <CloseIcon />
        </span>
      </div>
      <div class="modal__body">
        <NodeTree :selected-folder-id="selectedFolderIdLocal" @select="handleSelect" />
      </div>
      <div class="modal__footer">
        <Button :variant="'danger'" @click="closeModal">Закрыть</Button>
        <Button :variant="'primary'" @click="confirmSelection">Ок</Button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';
import NodeTree from '@/components/node-tree/NodeTree.vue';
import Button from '@/components/ui/Button.vue';
import CloseIcon from '@/components/icons/IconClose.vue';

const { title, selectedFolderId } = defineProps({
  title: String,
  selectedFolderId: Number,
});

const emit = defineEmits(['close', 'select']);

const selectedFolderIdLocal = ref<number | null>(selectedFolderId);

watch(() => selectedFolderId, (newVal) => {
  selectedFolderIdLocal.value = newVal;
});

const closeModal = () => {
  emit('close');
};

const handleSelect = (folderId: number) => {
  selectedFolderIdLocal.value = folderId;
};

const confirmSelection = () => {
  if (selectedFolderIdLocal.value !== null) {
    emit('select', selectedFolderIdLocal.value);
  }
  closeModal();
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal__overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
}

.modal__content {
  min-width: 300px;
  background: white;
  padding: 20px;
  border-radius: 5px;
  position: relative;
  z-index: 1;
}

.modal__header,
.modal__footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.modal__body {
  margin: 50px 0;
}
</style>
  