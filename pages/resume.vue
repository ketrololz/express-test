<template>
  <div class="flex flex-col gap-y-4">
    <ResumeDownload :items="buttons" />
    <ProfileInfo />
  </div>
</template>

<script setup lang="ts">
const id = ref(0)
const buttons = [
  {
    id: id.value++,
    icon: "i-heroicons-document-arrow-down",
  },
  {
    id: id.value++,
    label: "PDF",
  },
  {
    id: id.value++,
    label: "DOC",
  },
  {
    id: id.value++,
    icon: "i-heroicons-document-text-solid",
  },
  {
    id: id.value++,
    icon: "i-heroicons-trash",
  },
  {
    id: id.value++,
    icon: "i-heroicons-arrow-right-start-on-rectangle-20-solid",
  },
  {
    id: id.value++,
    icon: "i-heroicons-heart-20-solid",
  },
];
</script>
