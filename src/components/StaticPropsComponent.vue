<template>
  <div>
    <br />
    <br />
    <p>Received name: {{ props.name }}, from <b>App.vue</b>.</p>
    <p>This component demonstrates how to use props in Vue.js.</p>
  </div>
</template>

<script setup>
const props = defineProps(
  ['name']
)
</script>

<style></style>
