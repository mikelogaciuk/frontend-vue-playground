<template>
  <div>
    <br />
    <br />
    <input type="text" ref="myRef" placeholder="Type something" />
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const myRef = ref("")

onMounted(() => {
  // Component is mounted
  console.log(myRef.value);
  // You can access the DOM element or perform any setup logic here
  myRef.value.focus()
  myRef.value.value = "Hello, World!";
})
</script>

<style></style>
