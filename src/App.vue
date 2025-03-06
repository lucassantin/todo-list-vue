<script setup>
  import { ref, watch } from 'vue';

  const name = ref(localStorage.getItem('name') || '');

  const todos = ref(JSON.parse(localStorage.getItem('todos')) || []);
  const input_content = ref('');
  const input_category = ref('');

  const addTodo = () => {
    if ( input_content.value.trim() === '' || input_category.value === null) {
      return;
    }

    todos.value.push({
      content: input_content.value,
      category: input_category.value,
      done: false
    });

    input_content.value = '';
    input_category.value = null;
  }

  const removeTodo = (todo) => {
    todos.value = todos.value.filter((t) => t!== todo);
  }

  const toggleDone = (todo) => {
    todo.done = !todo.done;
  }

  watch(name, (newName) => {
    localStorage.setItem('name', newName);
  })

  watch(todos, (newVal) => {
	localStorage.setItem('todos', JSON.stringify(newVal))
}, {
	deep: true
})
</script>

<template>
  <main class="flex flex-col w-dvw h-screen p-8 gap-4">
    <section>
      <p class="text-4xl font-bold">What's up, <input class="w-44 " placeholder="Name here" type="text" v-model="name"></p>
    </section>
    <section class="flex flex-col gap-3">
      <div>
        <p class="text-2xl  font-semibold  text-stone-200">CREATE A TODO</p>
        <p class="text-stone-200">What's on your todo list?</p>
      </div>
      <input class="w-full p-2 bg-stone-800" type="text" placeholder="e.g. make a video" v-model="input_content" />
    </section>
    <section>
      <p class="pb-2 text-stone-200 text-2xl font-medium">Pick a category</p>
      <div class="grid grid-cols-2 gap-4">
        <label class="flex justify-center items-center bg-indigo-700 rounded-lg">
          <div  class="flex flex-col justify-center items-center gap-1.5 p-6">
            <input 
            class="w-6 h-6"
            type="radio" 
            name="category" 
            id="category1" 
            value="business"
            v-model="input_category" />
            <p class="text-3xl font-bold">Business</p>
          </div>
        </label>
        <label class="flex justify-center items-center bg-emerald-700 rounded-lg">
          <div  class="flex flex-col justify-center items-center gap-1.5 p-6 ">
            <input 
            class="w-6 h-6"
            type="radio" 
            name="category" 
            id="category1" 
            value="personal"
            v-model="input_category" />
            <p class="text-3xl font-bold">Personal</p>
          </div>
        </label>
      </div>
      <button @click="addTodo" class="w-full bg-stone-800 text-xl rounded-lg font-bold py-2 mt-4 active:bg-slate-700 active:scale-98 transition-transform">Add Todo</button>
    </section>
    <section>
      <p class="text-stone-200 text-2xl font-medium mb-4">Todo List</p>
      <div v-for="(todo, index) in todos" :key="index" :class="['flex flex-row items-center justify-between py-2 p-3 rounded-lg mb-3 w-full', todo.category === 'business' ? 'bg-indigo-700 opacity-90' : 'bg-emerald-700 opacity-90']">
        <input type="checkbox" :checked="todo.done" @change="toggleDone(todo)" class="size-6">
        <p class="text-lg font-medium break-all w-[87%]">{{ todo.content }}</p>
        <button @click="removeTodo(todo)" class="right-2 text-xl text-white font-semibold py-0.5 px-2.5 rounded-sm bg-red-600">Delete</button>
      </div>
    </section>
  </main>
</template>

