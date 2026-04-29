<template>
  <div>
    <q-list bordered>
      <q-item clickable v-for="m in 3" :key="m">
        <q-item-section>ภารกิจที่ {{ m }} (mock)</q-item-section>
        <q-item-section side><q-btn color="positive" label="ทำสำเร็จ" flat /></q-item-section>
      </q-item>
    </q-list>
  </div>
</template>

<script setup lang="ts">
// mock only
</script>
