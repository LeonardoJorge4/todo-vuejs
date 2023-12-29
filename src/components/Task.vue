<script setup lang="ts">
import { TaskProps } from '../@types/Task.type';

defineProps<{
  task: TaskProps;
  onDelete: (id: string) => void;
  onCheck: (id: string) => void;
}>();
</script>

<template>
  <div
    class="grid grid-cols-[1fr_24px] gap-4 bg-gray-800 p-4 rounded-lg border border-gray-700 w-full"
  >
    <div class="flex gap-4 items-start">
      <input
        type="checkbox"
        v-on:click="onCheck(task.id)"
      />
      <p
        :data-isDone="task.done"
        class="text-gray-100 font-medium text-sm data-[isDone=true]:line-through"
      >
        {{ task.name }}
      </p>
    </div>
    <button
      type="button"
      class="w-6 h-6"
      v-on:click="onDelete(task.id)"
    >
      <img
        src="../assets/trash.svg"
        alt="Delete task"
      />
    </button>
  </div>
</template>
