<template>
  <div>
    <EventChildComponent @customEvent="handleCustomEvent" />
  </div>
</template>

<script setup>
import EventChildComponent from './EventChildComponent.vue';

function handleCustomEvent(message) {
  console.log('Received:', message);
  alert(message); // Shows: Hello from child!
}

</script>

<style></style>
