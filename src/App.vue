<script setup lang="ts">
import Counter from './components/Counter.vue';
import Header from './components/Header.vue';
</script>

<template>
  <div class="flex flex-col h-screen">
    <Header />

    <main class="bg-gray-800 w-full flex-1">
      <section class="max-w-3xl mx-auto">
        <form
          action=""
          class="flex gap-2 mt-[-27px]"
        >
          <input
            type="text"
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

        <div class="mt-16">
          <div class="flex justify-between">
            <Counter
              type="blue"
              title="Tarefas criadas"
              :amount="0"
            />
            <Counter
              type="purple"
              title="Concluídas"
              :amount="0"
            />
          </div>

          <div
            class="mt-6 pt-6 flex flex-col items-center justify-center border-t border-gray-600"
          >
            <img src="./assets/clipboard.svg" />
            <p class="text-gray-500 text-center mt-4 text-lg">
              <b>Você ainda não tem tarefas cadastradas</b>
              <br />
              Crie tarefas e organize seus itens a fazer
            </p>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>
