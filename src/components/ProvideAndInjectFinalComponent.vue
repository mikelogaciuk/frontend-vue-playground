<template>
  <div>
    <br />
    <h2>Provide and Inject Final Component:</h2>
    <table class="d-table">
      <thead>
        <tr>
          <th>Type</th>
          <th>Model</th>
          <th>Manufacturer</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>{{ type }}</td>
          <td>{{ model }}</td>
          <td>{{ manufacturer }}</td>
        </tr>
      </tbody>
    </table>
    <br />
    <p>This component uses the values provided by the parent component.</p>
  </div>
</template>

<script setup>
import { inject } from 'vue';

const type = inject('type');
const model = inject('model');
const manufacturer = inject('manufacturer');
</script>

<style></style>
