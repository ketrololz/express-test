<template>
  <UAvatar></UAvatar>
</template>

<script setup lang="ts">
import type { ProfileInfo } from './types/profile-info.ts'
const info = ref<ProfileInfo>()
onMounted(async () => {
  try {
    const response = await fetch("https://dev.jobcart.ru/wp-json/test/v2/app");
    if (!response.ok) {
      throw new Error("Failed to fetch user data");
    }
    const data = await response.json()
    info.value = data
  } catch (err) {
    console.error("Error fetching user:", err);
  }
});
</script>