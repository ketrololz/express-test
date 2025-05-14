<template>
  <div class="flex gap-4">
    <img :src="avatar" @error="handleAvatarError" class="w-40 h-40 rounded-md"/>
    <div>
      <h2 class="text-xl font-bold">{{ info.name }}</h2>
      <p>Кандидат на вакансию: Frontend-разработчик</p>
      <p>Дата отклика: {{ info.date }}</p>
      <p>Возраст: {{ info.age || "не указан" }}</p>
      <a :href="`tel:+${ info.phone }`" class="flex items-center gap-x-1.5"><UIcon name="i-lucide-phone" /> {{ info.phone || "не указан" }}</a>
      <a :href="`mailto:${ info.email }`"class="flex items-center gap-x-1.5"><UIcon name="i-lucide-mail" /> {{ info.email || "не указан" }}</a>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { ProfileInfo } from './types/profile-info.ts'
const info = ref<ProfileInfo>()
const avatar = ref('')

onMounted(async () => {
  try {
    const response = await fetch("https://dev.jobcart.ru/wp-json/test/v2/app");
    if (!response.ok) {
      throw new Error("Failed to fetch user data");
    }
    const data = await response.json()

    if (data.photo) {
      avatar.value = data.photo
    }

    info.value = data
  } catch (err) {
    console.error("Error fetching user:", err);
  }
});

function handleAvatarError() {
  avatar.value = '/avatar.png';
}
</script>