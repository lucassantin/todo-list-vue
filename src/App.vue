<script setup>
  import { ref, watch } from 'vue';

  const name = ref(localStorage.getItem('name') || '');

  watch(name, (newName) => {
    localStorage.setItem('name', newName);
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
      <input class="w-full p-2 bg-stone-800" type="text" placeholder="e.g. make a video">
    </section>
    <section>
      <p>Pick a category</p>
      
    </section>
  </main>
</template>

<style scoped>

</style>
