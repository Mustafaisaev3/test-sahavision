<template>
  <div :class="['button', `button--${variant}`]" v-bind="$attrs">
    <slot />
  </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue';

type Variant = 'primary' | 'secondary' | 'danger';

const { variant } = defineProps<{
  variant: Variant;
}>();
</script>

<style scoped>
.button {
  min-width: 80px;
  text-align: center;
  border: none;
  border-radius: 24px;
  padding: 10px 16px;
  cursor: pointer;
}

.button--primary {
  color: white;
  background: rgb(48, 246, 98);
}

.button--secondary {
  color: white;
  background: gray;
}

.button--danger {
  color: white;
  background: rgb(213, 50, 50);
}
</style>  