<script setup lang="ts">
import { computed, ref } from 'vue';
import Counter from './components/Counter.vue';
import Header from './components/Header.vue';
import Task from './components/Task.vue';
import { TaskProps } from './@types/Task.type';

let tasksList = ref<TaskProps[]>([]);
const task = ref('');
const tasksDoneAmount = computed(
  () => tasksList.value.filter((task) => task.done).length
);

function addTask() {
  if (!task.value) {
    return alert('Informe o título da tarefa para criar!');
  }

  tasksList.value.push({
    id: String(new Date().getTime()),
    name: task.value,
    done: false,
  });
  task.value = '';
}

function handleToggleDoneTask(id: string) {
  tasksList.value = tasksList.value
    .map((item) => (item.id === id ? { ...item, done: !item.done } : item))
    .sort((a, b) => Number(b.done) - Number(a.done));
}

function deleteTask(id: string) {
  const taskIndex = tasksList.value.findIndex((task) => task.id === id);

  if (taskIndex < 0) {
    return alert('Tarefa não encontrada!');
  }

  tasksList.value.splice(taskIndex, 1);
}
</script>

<template>
  <Header />

  <main
    class="bg-gray-800 w-full h-[calc(100vh-10rem)] md:h-[calc(100vh-12rem)] px-4 pb-4 md:px-0"
  >
    <section class="max-w-3xl mx-auto h-full">
      <form
        @submit.prevent="addTask"
        class="flex gap-2 relative top-[-27px]"
      >
        <input
          type="text"
          v-model="task"
          placeholder="Adicione uma nova tarefa"
          class="bg-gray-700 h-[54px] p-4 text-gray-300 rounded-lg border-none flex-1 focus:outline-none"
        />
        <button
          type="submit"
          class="flex gap-2 bg-blue-800 items-center h-[54px] rounded-lg focus:outline-none p-4"
        >
          <span class="font-semibold text-sm text-gray-100">Criar</span>
          <img src="./assets/plus.svg" />
        </button>
      </form>

      <div class="mt-8">
        <div class="flex justify-between">
          <Counter
            type="blue"
            title="Tarefas criadas"
            :amount="tasksList.length"
          />
          <Counter
            type="purple"
            title="Concluídas"
            :amount="tasksDoneAmount"
          />
        </div>

        <div
          class="mt-6 pt-6 flex flex-col items-center justify-center border-t border-gray-600"
        >
          <div v-if="!tasksList.length">
            <img
              src="./assets/clipboard.svg"
              class="mx-auto"
            />
            <p class="text-gray-500 text-center mt-4 text-lg">
              <b>Você ainda não tem tarefas cadastradas</b>
              <br />
              Crie tarefas e organize seus itens a fazer
            </p>
          </div>

          <div
            v-else
            class="w-full flex flex-col gap-4 overflow-y-auto h-[42vh]"
          >
            <Task
              v-for="task in tasksList"
              :key="task.id"
              :task="task"
              :onDelete="deleteTask"
              :onCheck="handleToggleDoneTask"
            />
          </div>
        </div>
      </div>
    </section>
  </main>
</template>
