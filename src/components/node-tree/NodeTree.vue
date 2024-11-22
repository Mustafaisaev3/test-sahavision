<template>
  <div class="node-tree">
    <NodeTreeItem
      v-for="node in folders"
      :key="node.id"
      :node-item="node"
      :selected-folder-id="selectedFolderId"
      @select="handleSelect"
    />
  </div>
</template>

<script setup lang="ts">
import type { INode } from '@/types';
import NodeTreeItem from '@/components/node-tree/NodeTreeItem.vue';

const { selectedFolderId } = defineProps({
  selectedFolderId: Number,
});

const folders: INode[] = [
  { id: 1, name: 'Папка 1', children: [
    { id: 2, name: 'Папка 1.1', children: [] },
    { id: 3, name: 'Папка 1.2', children: [
      { id: 4, name: 'Папка 1.2.1', children: [] }
    ]}
  ]},
  { id: 5, name: 'Папка 2', children: [] },
];

const emit = defineEmits(['select']);

const handleSelect = (folderId: number) => {
  emit('select', folderId);
};
</script>

<style scoped>
.node-tree {
  display: flex;
  flex-direction: column;
  gap: 5px;
}
</style>
