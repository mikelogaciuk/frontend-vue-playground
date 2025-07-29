# Vue Notes

## Components

A component is a reusable piece of code that encapsulates its own structure, style, and behavior. Components can be nested, reused, and managed independently.

They are like a `lego blocks` that can be combined to build complex user interfaces.

Example:

```vue
// MyComponent.vue
<script setup>
// JavaScript logic for the component
</script>

<template>
  // HTML structure of the component
  <div>
    <h1>Hello, World!</h1>
  </div>
</template>

<style scoped>
// Scoped styles for this component
</style>
```

## Text Interpolation

Text interpolation is a way to display dynamic data in the template. It allows you to embed JavaScript expressions within the template.

Example:

````vue
<script setup>
const message = 'Hello, Vue!'
</script>

<template>
  <div>
    <p>{{ message }}</p>
  </div>
</template>

## Attribute Binding Attribute binding allows you to bind data to HTML attributes dynamically. You
can use the `v-bind` directive or the shorthand `:` to bind attributes. Where the `:` is the new
shorthand for `v-bind`. Example: ```vue
<script setup>
const compaanySite = 'https://mediaexpert.pl/'
const alternateName = 'TERG S.A.'
const name = 'Mike'
const age = 18
</script>

<template>
  <div>
    <a :href="compaanySite">Media Expert or so called {{ alternateName }}</a>
    <br /><br />
    <p>My name is {{ name }} and I am {{ age }} years old (joking).</p>
  </div>
</template>
````

## Reactivity

Reactivity in Vue allows the UI to automatically update when the underlying data changes. Vue uses a reactive system that tracks dependencies and updates the DOM efficiently.

We have to use `ref` or `reactive` to create reactive data. The `ref` is used for primitive values, while `reactive` is used for objects and arrays.

### Reactive

A reactive object is an object that Vue can track for changes. When a property of a reactive object changes, Vue automatically updates the DOM to reflect that change.

Example:

```vue
<script setup>
import { reactive } from 'vue'

const state = reactive({
  skills: ['DevOps', 'DataOps', 'SREOps', 'Architecture', 'Backend'],
})

const addSkill = () => {
  if (state.skills.includes('Vue.js')) return
  state.skills.push('Vue.js')
}
</script>

<template>
  <div>
    <br />
    <button class="d-btn d-btn-accent" @click="addSkill">Add new skill below... (ha!)</button>
    <p>Skills: {{ state.skills.join(', ') }}</p>
    <br />
  </div>
</template>
```

The `reactive` can't store primitive values (e.g., numbers, strings, booleans), so we have to use `ref` for that.

### Ref

A `ref` is a reactive reference to a primitive value. When the value of a `ref` changes, Vue automatically updates the DOM to reflect that change.

Example:

```vue
<script setup>
import { ref } from 'vue'

const age = ref(18)
</script>
<template>
  <div>
    <p>My age is {{ age }}</p>
    <button class="d-btn d-btn-accent" @click="age++">Increase Age</button>
  </div>
</template>
```

It is widely used for single values like numbers, strings, and booleans. It can also be used to create reactive references to DOM elements.

## Computed Properties

Computed properties are a powerful feature in Vue that allow you to define properties that depend on other reactive properties. They are automatically updated when their dependencies change.

Example:

```vue
<script setup>
import { computed, ref } from 'vue'

const firstName = ref('John')
const lastName = ref('Doe')

const fullName = computed(() => {
  return `${firstName.value} ${lastName.value}`
})
</script>

<template>
  <div>
    <p>Full Name: {{ fullName }}</p>
  </div>
</template>
```

## Conditional Rendering

Conditional rendering allows you to display or hide elements based on certain conditions. You can use the `v-if`, `v-else-if`, and `v-else` directives to control the rendering of elements.

Example:

```vue
<script setup>
import { ref } from 'vue'

const isLoggedIn = ref(false)
</script>

<template>
  <div>
    <p v-if="isLoggedIn">Welcome back!</p>
    <p v-else>Please log in.</p>
    <button class="d-btn d-btn-soft d-btn-warning" @click="isLoggedIn = !isLoggedIn">
      Toggle Login Status
    </button>
  </div>
</template>
```

### List Rendering

List rendering allows you to render a list of items using the `v-for` directive. You can iterate over arrays or objects and generate a list of elements.

Example:

```vue
<script setup>
import { ref } from 'vue'

const people = ref(['Alice', 'Bob', 'Charlie'])
const stock = ref([
  { sku: 'SKU123', quantity: 10 },
  { sku: 'SKU456', quantity: 5 },
  { sku: 'SKU789', quantity: 0 },
])
</script>

<template>
  <div>
    <ul>
      <li v-for="person in people">{{ person }}</li>
    </ul>
  </div>
</template>
```

But this is not sub-optimal, because we are not using the `key` attribute. The `key` attribute is used to give each item a unique identifier, which helps Vue optimize rendering and maintain state. Without that, Vue will not be able to track the items properly, which can lead to performance issues and bugs and full DOM re-rendering.

So when using big volumes of data, we should always use the `key` attribute:

```html
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
```

## Propeties

### Static props

Propeties aka `props` are a way to pass data from a parent component to a child component. They allow you to make components reusable and configurable.

```vue
<script setup>
import { defineProps } from 'vue'

const props = defineProps(['name'])
</script>
<template>
  <div>
    <p>Hello, {{ props.name }}!</p>
  </div>
</template>
```

### Dynamic props

Dynamic props allow you to pass data to a component using the `v-bind` directive or the shorthand `:`. This is useful when you want to bind a variable or an expression to
a prop.

```

```
