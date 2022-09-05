<template>
  <div :class="spanClass">
    <slot></slot>
  </div>
</template>

<script lang="ts" setup>
import { computed } from 'vue';

const props = defineProps({
  span: {
    type: Number,
    required: false
  }
});

const spanClass = computed(() => props.span ? `col-span-${props.span}` : "");
</script>
