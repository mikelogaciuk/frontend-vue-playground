<template>
  <div>
    <br />
    <fieldset class="d-fieldset bg-base-300 border-base-300 rounded-box w-xs p-4">
      <br />
      <h1 class="text-2xl">{{ message }}</h1>
      <br />
      <br />
      <input v-model="inputValue" class="d-input-accent border-accent" placeholder="Type something..." />
    </fieldset>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const message = ref('Hi!');
const inputValue = ref('');

watch(inputValue, (newValue, oldValue) => {
  message.value = `You typed: ${newValue}`;
})
</script>

<style></style>
