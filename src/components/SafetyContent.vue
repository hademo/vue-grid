<template>
  <div>
    <div class="header" @click="isCollapsed = !isCollapsed">
      <slot name="header"></slot>
    </div>


    <VGrid :size="1" :gap="gap" v-if="!isCollapsed">
      <VGrid :size="size" :gap="gap">
        <slot name="columns"></slot>
      </VGrid>

      <VGrid v-for="item in items" :size="size" :gap="gap">
        <slot name="item" v-bind="item">
        </slot>
      </VGrid>
    </VGrid>
  </div>
</template>

<script lang="ts" setup>
import { PropType, ref } from 'vue';
import VGrid from './VGrid.vue'

const isCollapsed = ref(false);

const props = defineProps({
  size: {
    type: Number,
    required: true
  },
  gap: {
    type: Number,
    required: false
  },
  items: {
    type: Array as PropType<Array<any>>,
    required: true
  }
});
</script>

<style>
.header {
  @apply bg-green-500 mb-2 cursor-pointer
}
</style>
