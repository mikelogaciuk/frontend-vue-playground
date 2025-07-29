<script setup>
const message = 'Hello, from Vue!'
const happyNumber = Math.random().toPrecision(2) * 100
</script>

<template>
  <div>
    <h1>{{ message }} While today is a happy number of: {{ happyNumber }}</h1>
    <p>This is a simple Vue component.</p>
    <p>I work for:</p>
  </div>
</template>

<style scoped></style>
