<template>
  <div>
    <DynamicPropsComponent :sales="sales" :revenue="revenue" :profit="profit" />
  </div>
</template>

<script setup>
import DynamicPropsComponent from './DynamicPropsComponent.vue';
import { ref } from 'vue';
const sales = ref(366666.99)
const revenue = ref(500000.00);
const profit = ref(133333.01);
</script>

<style></style>
