<template>
  <div>
    <br />
    <p v-if="isLoggedIn">Welcome back!</p>
    <p v-else>Please log in.</p>
    <button class="d-btn d-btn-soft d-btn-error rounded-2xl" @click="toggleLogin">
      Toggle Login Status
    </button>
    <p v-show="isVisible">This text is visible or not based on a value of <b>isVisible</b></p>
    <button class="d-btn d-btn-soft d-btn-primary rounded-2xl" @click="toggleVisibility">
      Toggle Visibility
    </button>
    <br />
    The list of people without a key:
    <ul>
      <li v-for="person in people"> - {{ person }}</li>
    </ul>
    <br />
    The table of SKU's with a key:
    <table class="d-table d-table-striped">
      <thead>
        <tr>
          <th>SKU</th>
          <th>Quantity</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in stock" :key="index">
          <td>{{ item.sku }}</td>
          <td>{{ item.quantity }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const isLoggedIn = ref(false)

const toggleLogin = () => {
  isLoggedIn.value = !isLoggedIn.value
}

const isVisible = ref(true)
const toggleVisibility = () => {
  isVisible.value = !isVisible.value
}

const people = ref(["Alice", "Bob", "Charlie"])
const stock = ref([
  { sku: "SKU123", quantity: 10 },
  { sku: "SKU456", quantity: 5 },
  { sku: "SKU789", quantity: 0 }
])
</script>

<style></style>
