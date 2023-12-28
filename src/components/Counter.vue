<script setup lang="ts">
defineProps<{ title: string; amount: number; type: 'purple' | 'blue' }>();
</script>

<template>
  <div class="flex gap-2">
    <span
      :data-type="type"
      class="font-semibold text-gray-200 data-[type=purple]:text-purple-700 data-[type=blue]:text-blue-500"
      >{{ title }}</span
    >
    <div class="bg-gray-500 text-gray-200 font-semibold px-2 rounded-full">
      {{ amount }}
    </div>
  </div>
</template>
