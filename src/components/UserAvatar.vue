<template>
  <q-avatar :size="size + 'px'" color="primary">
    <q-icon name="person" size="md" />
  </q-avatar>
</template>

<script setup lang="ts">
defineProps<{ size?: number }>();
</script>
