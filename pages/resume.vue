<template>
  <ResumeDownload :items="buttons"></ResumeDownload>
</template>

<script setup lang="ts">
const buttons = [
  {
    icon: "i-heroicons-document-arrow-down",
  },
  {
    label: "PDF",
  },
  {
    label: "DOC",
  },
  {
    icon: "i-heroicons-document-text-solid",
  },
  {
    icon: "i-heroicons-trash",
  },
  {
    icon: "i-heroicons-arrow-right-start-on-rectangle-20-solid",
  },
  {
    icon: "i-heroicons-heart-20-solid",
  },
];
</script>
