<template>
  <div>
    <br />

    <button class="d-btn d-btn-error" @click="notifyParent">Click Me</button>
  </div>
</template>

<script setup>
const emit = defineEmits(['customEvent']);

function notifyParent() {
  emit('customEvent', 'Hello from child!');
}

</script>

<style></style>
