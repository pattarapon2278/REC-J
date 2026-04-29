<template>
  <div>
    <div class="q-mb-md">(mock) ข้อความแชทจะแสดงที่นี่</div>
    <q-input filled v-model="message" label="พิมพ์ข้อความ..." />
    <q-btn color="primary" label="ส่ง" class="q-mt-sm" @click="sendMessage" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const message = ref('');

function sendMessage() {
  if (!message.value.trim()) {
    return;
  }
  message.value = '';
}
</script>
