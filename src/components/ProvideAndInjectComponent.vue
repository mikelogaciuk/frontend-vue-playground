<template>
  <ProvideAndInjectLoaderComponent />
</template>

<script setup>
import ProvideAndInjectLoaderComponent from './ProvideAndInjectLoaderComponent.vue';
import { provide } from 'vue';

provide('type', 'Airliner')
provide('model', 'MD-11');
provide('manufacturer', 'McDonnell Douglas');
</script>

<style></style>
