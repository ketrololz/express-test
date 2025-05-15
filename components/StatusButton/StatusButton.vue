<template>
  <div class="flex">
    <UButton
      class="rounded-l-md rounded-r-none px-6 h-11"
      size="xs"
      :variant="isActive ? 'solid' : 'outline'"
      color="neutral"
      @click="toggleDisable"
      >{{ text }}</UButton
    >
    <div class="arrow-tip bg-{--ui-primary}" color="neutral"/>
  </div>
</template>

<script setup lang="ts">
const isActive = ref(false);

defineProps<{
  text: string;
}>();

function toggleDisable() {
  isActive.value = !isActive.value;
}
</script>

<style scoped>
.arrow-tip {
  width: 0;
  height: 0;
  border-top: 22px solid transparent;
  border-bottom: 22px solid transparent;
  border-left: 14px solid;
}
</style>
