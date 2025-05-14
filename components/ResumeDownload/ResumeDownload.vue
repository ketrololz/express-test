<template>
  <div class="flex gap-x-1">
    <UButton v-for="item of props.items"
      color="primary"
      variant="outline"
      class="flex justify-center w-10 p-2"
    >
      <UIcon v-if="item.icon" :name="item.icon" class="!size-6"></UIcon
    >{{ item.label }}</UButton>
  </div>
</template>

<script setup lang="ts">
import type { ButtonsProps } from "./types/buttons-props.ts";
const props = defineProps<{
  items: ButtonsProps[];
}>();
</script>
