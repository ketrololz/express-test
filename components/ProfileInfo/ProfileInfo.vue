<template>
  <div class="flex gap-4">
    <img
      :src="avatar"
      @error="handleAvatarError"
      class="w-45 h-45 rounded-md"
    />
    <div>
      <h2 class="text-xl font-bold">{{ info?.name }}</h2>
      <p>Кандидат на вакансию: Frontend-разработчик</p>
      <p>{{ info?.status === "viewed" ? "Просмотрено" : "Не просмотрено" }}</p>
      <p>Дата отклика: {{ info?.date }}</p>
      <p>Возраст: {{ info?.age || "не указан" }}</p>
      <a :href="`tel:+${info?.phone}`" class="flex items-center gap-x-1.5"
        ><UIcon name="i-lucide-phone" /> {{ info?.phone || "не указан" }}</a
      >
      <a :href="`mailto:${info?.email}`" class="flex items-center gap-x-1.5"
        ><UIcon name="i-lucide-mail" /> {{ info?.email || "не указан" }}</a
      >
    </div>
  </div>
  <div class="flex flex-col gap-2">
    <p>Дела:</p>
    <div class="flex gap-x-2">
      <UButton
        @click="switchInterviewStatus"
        :color="interviewStatus ? 'success' : 'error'"
        class="max-w-40"
        >{{ interviewStatusText }}</UButton
      >
      <UButton class="max-w-40">Создать видеозвонок</UButton>
      <UButton class="max-w-40">Запланировать событие</UButton>
      <UButton class="max-w-30">Отправить запрос</UButton>
    </div>
  </div>
  <div class="flex flex-col gap-2">
    <p>Статус рассмотрения:</p>
    <div class="flex gap-2 max-w-300 flex-wrap w-full">
      <StatusButton v-for="item of statusItems" :key="item.id" :text="item.text"/>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { ProfileInfo } from "./types/profile-info.ts";
const info = ref<ProfileInfo>();
const avatar = ref("");
const interviewStatus = ref(false);
const interviewStatusText = computed(() => {
  return interviewStatus.value
    ? "Собеседование запланировано"
    : "Собеседование не запланировано";
});

onMounted(async () => {
  try {
    const response = await fetch("https://dev.jobcart.ru/wp-json/test/v2/app");
    if (!response.ok) {
      throw new Error("Failed to fetch user data");
    }
    const data = await response.json();

    if (data.photo) {
      avatar.value = data.photo;
    }

    info.value = data;
  } catch (err) {
    console.error("Error fetching user:", err);
  }
});

const id = ref(0)
const statusItems = [
  {
    id: id.value++,
    text: 'Новое',
  },
  {
    id: id.value++,
    text: 'Просмотрено',
  },
  {
    id: id.value++,
    text: 'Отправлено приглашение',
  },
  {
    id: id.value++,
    text: 'Назначено собеседование',
  },
  {
    id: id.value++,
    text: 'Не дошел',
  },
  {
    id: id.value++,
    text: 'Проведено собеседование',
  },
  {
    id: id.value++,
    text: 'Ожидание ответа соискателя',
  },
  {
    id: id.value++,
    text: 'Принятие решения',
  },
  {
    id: id.value++,
    text: 'Принят',
  },
  {
    id: id.value++,
    text: 'Отклонено/Отказ',
  },
  {
    id: id.value++,
    text: 'Архивировано',
  },
];

function handleAvatarError() {
  avatar.value = "/avatar.png";
}

function switchInterviewStatus() {
  interviewStatus.value = !interviewStatus.value;
}
</script>
