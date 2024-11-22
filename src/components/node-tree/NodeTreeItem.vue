<template>
  <div class="node-item">
    <div
      :class="[
        'node-item__wrapper',
        { 'node-item__wrapper--no-children': !nodeItem?.children?.length },
        { 'node-item__wrapper--selected': nodeItem.id === selectedFolderId }
      ]"
      @click="selectFolder"
    >
      <span
        :class="[
          'node-item__icon',
          { 'node-item__icon--open': isOpen }
        ]"
        v-if="nodeItem?.children?.length"
        @click.stop="toggleOpen"
      >
        <ChevronRight />
      </span>
      <span class="node-item__name">
        {{ nodeItem?.name }}
      </span>
    </div>
    <div
      class="node-item__children"
      v-if="isOpen && nodeItem?.children"
    >
      <NodeTreeItem
        v-for="childNodeItem in nodeItem?.children"
        :key="childNodeItem.id"
        :node-item="childNodeItem"
        :selected-folder-id="selectedFolderId"
        @select="handleSelect"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import type { INode } from '@/types/index';
import type { PropType } from 'vue';

import ChevronRight from '../icons/IconChevronRight.vue';

const { nodeItem, selectedFolderId } = defineProps({
  nodeItem: Object as PropType<INode>,
  selectedFolderId: Number,
});

const emit = defineEmits(['select']);

const isOpen = ref(false);
const toggleOpen = () => {
  isOpen.value = !isOpen.value;
};

const selectFolder = () => {
  emit('select', nodeItem.id);
};

const handleSelect = (folderId: number) => {
  emit('select', folderId);
};
</script>

<style scoped>
.node-item {
  padding-left: 20px;
}

.node-item__wrapper {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.node-item__wrapper--no-children {
  padding-left: 20px;
}

.node-item__wrapper--selected {
  background-color: #e0e0e0;
}

.node-item__icon {
  width: 20px;
  display: flex;
  align-items: center;
}

.node-item__icon--open {
  transform: rotate(45deg);
}

.node-item__name {
  display: flex;
  align-items: center;
}
</style>