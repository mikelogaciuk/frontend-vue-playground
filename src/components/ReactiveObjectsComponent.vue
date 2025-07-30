<script setup>
import { computed, reactive, ref } from 'vue';

const ageState = reactive({
  age: { value: 18 }
})

const skillsState = reactive({
  skills: ['DevOps', 'DataOps', 'SREOps', 'Architecture', 'Backend', 'POS', 'ERP', 'Data Engineering'],
})

const state = reactive({
  languages: ['Python', 'Ruby', 'Elixir', 'Javascript', 'Typescript', 'Go']
})

const addSkill = () => {
  if (skillsState.skills.includes('Vue.js')) return;
  skillsState.skills.push('Vue.js');
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

  <p>My name is <b>{{ name }}</b> and I am <b>{{ ageState.age.value }}</b> years old (joking), but you can randomize my
    name using <button class="d-btn d-btn-soft d-btn-info rounded-3xl" @click="randomizeName">this</button>.
    <br />To make my computed fullname as: <b>{{ fullName }}</b>.
    <br /> <br />
    The garbage below was done for <b>Vue learning purposes</b>. <br />
    Since last time I wrote front-end, 20 or more years passed. In that moment there was even no Node.js.
    <br />
    Everything was done using Php inside .php files and the Ruby and Rails
    was not even a thing. No one dreamed about Vue.js, React.js, Angular.js or any other thing like that.
  </p>

  <br />
  <h1>You can increase or decrease my age:</h1>
  <button class="d-btn d-btn-info" @click="ageState.age.value++">Increase age</button>
  <button class="d-btn d-btn-error" @click="ageState.age.value--">Decrease age</button>

  <br /> <br />

  <p>Skills: {{ skillsState.skills.join(', ') }}</p>
  <button class="d-btn d-btn-accent" @click="addSkill">Add new skill...
    (ha!)</button>

  <p>The one of my favorite languages is <b>{{ randomLanguage() }}</b> and this will change also when you click age
    increase or decrease, because of <i>randomLanguage()</i> function that is invoked everytime the DOM reloads.</p>
</template>

<style></style>
