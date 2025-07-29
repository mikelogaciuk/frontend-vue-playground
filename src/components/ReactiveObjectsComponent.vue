<script setup>
import { computed, reactive, ref } from 'vue';

const state = reactive({
  age: { value: 18 },
  skills: ['DevOps', 'DataOps', 'SREOps', 'Architecture', 'Backend', 'POS', 'ERP', 'Data Engineering'],
  languages: ['Python', 'Ruby', 'Elixir', 'Javascript', 'Typescript', 'Go']
})

const addSkill = () => {
  if (state.skills.includes('Vue.js')) return;
  state.skills.push('Vue.js');
}

const randomLanguage = () => {
  const randomIndex = Math.floor(Math.random() * state.languages.length);
  return state.languages[randomIndex];
}

const name = ref('Mike')
const lastName = ref('Logan')

const fullName = computed(() => {
  return `${name.value} ${lastName.value}`;
});

const randomizeName = () => {
  const names = ['Mike', 'Kasper', 'Alice', 'Vermheer'];
  const randomIndex = Math.floor(Math.random() * names.length);
  name.value = names[randomIndex];
}
</script>

<template>

  <p>My name is <b>{{ name }}</b> and I am <b>{{ state.age.value }}</b> years old (joking), but you can randomize my
    name using <button class="d-btn d-btn-soft d-btn-info rounded-3xl" @click="randomizeName">this</button>.
    <br />To make my computed fullname as: <b>{{ fullName }}</b>.
    <br /> <br />
    The garbage below was done for <b>Vue learning purposes</b>. <br />
    Since last time I wrote front-end, 20 years passed. In that moment there was even no Node.js.
    <br />
    Everything was done using .Php or vanilla JavaScript and Ruby and Rails was initial getting attention.
  </p>

  <br />
  <h1>You can increase or decrease my age:</h1>
  <button class="d-btn d-btn-info" @click="state.age.value++">Increase age</button>
  <button class="d-btn d-btn-error" @click="state.age.value--">Decrease age</button>

  <br /> <br />

  <p>Skills: {{ state.skills.join(', ') }}</p>
  <button class="d-btn d-btn-accent" @click="addSkill">Add new skill...
    (ha!)</button>

  <p>The one of my favorite languages is <b>{{ randomLanguage() }}</b>.</p>
</template>

<style></style>
