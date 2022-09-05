<template>
  <div :class="[gridClass, gapClass]">
    <slot></slot>
  </div>
</template>

<script lang="ts" setup>
import { computed } from '@vue/reactivity';

const props = defineProps({
  size: {
    type: Number,
    required: true
  },
  gap: {
    type: Number,
    required: false
  }
});

const gridClass = computed(() => `grid grid-cols-${props.size}`);
const gapClass = computed(() => props.gap ? `gap-${props.gap}` : "");
</script>
