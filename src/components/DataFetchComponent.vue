<template>
  <div>
    <br />
    <br />
    <button class="d-btn d-btn-success" @click="fetchData">Fetch Data</button>
    <div v-if="data">
      <h2>Fetched Data:</h2>
      <pre>{{ data }}</pre>
    </div>
    <div v-else>
      <p>No data fetched yet.</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const data = ref(null);

const fetchData = () => {
  fetch('https://jsonplaceholder.typicode.com/posts/1')
    .then((response) => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then((responseData) => {
      data.value = responseData;
    })
    .catch((error) => {
      console.error('There has been a problem with your fetch operation:', error);
    });
}
</script>

<style></style>
