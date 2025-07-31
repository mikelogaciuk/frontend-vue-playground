# Vue Notes

- [Vue Notes](#vue-notes)
  - [Components](#components)
  - [Text Interpolation](#text-interpolation)
  - [Reactivity](#reactivity)
    - [Reactive](#reactive)
    - [Ref](#ref)
    - [Ref vs Reactive pitfalls](#ref-vs-reactive-pitfalls)
  - [Computed Properties](#computed-properties)
  - [Conditional Rendering](#conditional-rendering)
    - [List Rendering](#list-rendering)
  - [Propeties](#propeties)
    - [Static props](#static-props)
    - [Dynamic props](#dynamic-props)
  - [Slots](#slots)
  - [Fallback Defaults](#fallback-defaults)
  - [Named Slots](#named-slots)
  - [Provide \& Inject](#provide--inject)
    - [Provide](#provide)
    - [Inject](#inject)
    - [Provide and Inject Example](#provide-and-inject-example)
  - [Watchers](#watchers)
  - [Template Refs](#template-refs)
  - [Fetching Data](#fetching-data)
  - [Events](#events)
  - [Lifecycle Hooks](#lifecycle-hooks)
    - [Common Lifecycle Hooks](#common-lifecycle-hooks)
  - [Vue Router](#vue-router)
    - [Basic Usage](#basic-usage)
  - [Layouts](#layouts)
    - [Grid](#grid)
    - [Flexbox](#flexbox)
    - [Full-page / view-port scroll](#full-page--view-port-scroll)
  - [Note](#note)

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

### Ref vs Reactive pitfalls

In Vue 3, both `ref()` and `reactive()` are used for reactivity, but they have different **use** cases:

`ref()` as already mentioned is typically used for primitive values (like numbers, strings, booleans), but it can also wrap objects and arrays.

When you use `ref()` with an object or array, you access the value via .value. This is often suggested because `ref()` works consistently in both the `<script setup></script>` and `<template></template>`, and is easier to destructure without losing reactivity.

The `reactive()` is designed for objects and arrays, making all their properties reactive. However, destructuring a reactive object can break reactivity, which can lead to bugs if not handled carefully.

This is why, for example CoPilot suggests `ref()` for objects/arrays all the time.

In short:

- ref() is more predictable when passing objects/arrays as props or emitting them in events.
- ref() is compatible with Vue’s Composition API patterns and works well with TypeScript.

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

Dynamic props allow you to pass data to a component using the `v-bind` directive or the shorthand `:`. This is useful when you want to bind a variable or an expression to a prop.

`DynamicPropsLoaderComponent.vue`:

```vue
<template>
  <div>
    <DynamicPropsComponent :sales="sales" :revenue="revenue" :profit="profit" />
  </div>
</template>

<script setup>
import DynamicPropsComponent from './DynamicPropsComponent.vue'
import { ref } from 'vue'
const sales = ref(366666.99)
const revenue = ref(500000.0)
const profit = ref(133333.01)
</script>

<style></style>
```

`DynamicPropsComponent.vue`:

```vue
<template>
  <div>
    <br />
    <p>
      This is a dynamic props component.
      <br />
      It receives the following stats:
    </p>
    <br />
    <div class="d-stats bg-base-100 border-base-200 rounded-xs border">
      <div class="d-stat">
        <div class="d-stat-title">Sales</div>
        <div class="d-stat-value">
          {{ props.sales.toLocaleString('en-US', { style: 'currency', currency: 'USD' }) }}
        </div>
      </div>
      <div class="d-stat text-secondary">
        <div class="d-stat-title">Revenue</div>
        <div class="d-stat-value">
          {{ props.revenue.toLocaleString('en-US', { style: 'currency', currency: 'USD' }) }}
        </div>
      </div>
      <div class="d-stat">
        <div class="d-stat-title">Profit</div>
        <div class="d-stat-value">
          {{ props.profit.toLocaleString('en-US', { style: 'currency', currency: 'USD' }) }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps(['sales', 'revenue', 'profit'])
</script>

<style></style>
```

**Please note** that the `props` are immutable by default, meaning you cannot change their values directly within the child component. If you need to modify the data, you should emit an event to the parent component to handle the change.

## Slots

Slots are a way to create reusable components with customizable content. They allow you to define placeholders in a component's template that can be filled with content from the parent component.

In other terms, they are a space in a component where you can put various different things.

It allows to accept different content while maintaining the structure of the component.

`SlotComponent.vue`:

```vue
<template>
  <slot>
    <!-- Default slot content if no content is passed -->
    <br />
    <div class="default-slot-content">Default slot content goes here:</div>
  </slot>
</template>

<script setup></script>

<style></style>
```

`App.vue`:

```vue
<script setup>
import SlotComponent from './components/SlotComponent.vue'
</script>

<template>
  <SlotComponent>
    <p>This is content passed to the slot.</p>
  </SlotComponent>
</template>

<style></style>
```

## Fallback Defaults

You can also provide fallback content for slots. If no content is passed to the slot, the fallback content will be displayed.

It is good for example for a dashboard components that would display a message like "No data available" if no data is passed to it or loading spinner if data is being fetched.

`FallbackDefaultComponent.vue`:

```vue
<template>
  <br />
  <slot>
    <h1>Default Fallback Content</h1>
  </slot>
</template>

<script setup></script>

<style></style>
```

`App.vue`:

```vue
<script setup>
import FallbackDefaultComponent from './components/FallbackDefaultComponent.vue'
</script>

<template>
  <FallbackDefaultComponent> </FallbackDefaultComponent>
  <FallbackDefaultComponent>
    <h1>Custom Fallback Content using Fallback Component</h1>
  </FallbackDefaultComponent>
</template>

<style></style>
```

## Named Slots

Named slots allow you to define multiple slots within a single component, each with a unique name. This is useful when you want to provide different content for different parts of the component.

`NamedSlotComponent.vue`:

```vue
<template>
  <br />
  <slot name="upper"></slot>
  <slot></slot>
  <slot name="lower"></slot>
</template>

<script setup></script>

<style></style>
```

`App.vue`:

```vue
<script setup>
import NamedSlotComponent from './components/NamedSlotComponent.vue'
</script>

<template>
  <NamedSlotComponent>
    <template #upper>
      <h1>Upper Slot Content</h1>
    </template>
    <template #lower>
      <h2>Lower Slot Content</h2>
    </template>
  </NamedSlotComponent>
</template>

<style></style>
```

## Provide & Inject

Provide and inject are used to pass data from a parent component to deeply nested child components without having to pass props through every level of the component hierarchy.

### Provide

The `provide` option allows a parent component to provide data that can be injected by its descendants.

### Inject

The `inject` option allows a child component to access data provided by its ancestor components.

### Provide and Inject Example

`ProvideAndInjectComponent.vue`:

```vue
<template>
  <ProvideAndInjectLoaderComponent />
</template>

<script setup>
import ProvideAndInjectLoaderComponent from './ProvideAndInjectLoaderComponent.vue'
import { provide } from 'vue'

provide('type', 'Airliner')
provide('model', 'MD-11')
provide('manufacturer', 'McDonnell Douglas')
</script>
```

`ProvideAndInjectLoaderComponent.vue`:

```vue
<template>
  <ProvideAndInjectFinalComponent />
</template>

<script setup>
import ProvideAndInjectFinalComponent from './ProvideAndInjectFinalComponent.vue'
</script>

<style></style>
```

`ProvideAndInjectFinalComponent.vue`:

```vue
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
import { inject } from 'vue'

const type = inject('type')
const model = inject('model')
const manufacturer = inject('manufacturer')
</script>

<style></style>
```

## Watchers

Watchers are used to perform side effects in response to changes in reactive data. They allow you to execute code when a specific piece of data changes.

The watchers syntax is as follows: `watch(source, callback, options)`.

The `source` can be a reactive reference, a computed property, or an array of reactive references. The `callback` is a function that will be called when the source changes, and the `options` object can be used to configure the watcher like `immediate` and `deep` or `flush` and `onTrack/onTrigger`.

Example:

```vue
<template>
  <div>
    <br />
    <fieldset class="d-fieldset bg-base-300 border-base-300 rounded-box w-xs p-4">
      <br />
      <h1 class="text-2xl">{{ message }}</h1>
      <br />
      <br />
      <input
        v-model="inputValue"
        class="d-input-accent border-accent"
        placeholder="Type something..."
      />
    </fieldset>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

const message = ref('Hi!')
const inputValue = ref('')

watch(inputValue, (newValue, oldValue) => {
  message.value = `You typed: ${newValue}`
})
</script>

<style></style>
```

## Template Refs

This is a way to create a reference to a DOM element or a component instance in the template. It allows you to access the element or component directly in the script.

Example:

```vue
<template>
  <div>
    <br />
    <br />
    <input type="text" ref="myRef" placeholder="Type something" />
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'

const myRef = ref('')

onMounted(() => {
  // Component is mounted
  console.log(myRef.value)
  // You can access the DOM element or perform any setup logic here
  myRef.value.focus()
  myRef.value.value = 'Hello, World!'
})
</script>

<style></style>
```

## Fetching Data

Fetching data in Vue can be done using the `fetch` API or any other HTTP client like Axios. You can use the `onMounted` lifecycle hook to fetch data when the component is mounted:

```vue
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
import { ref } from 'vue'

const data = ref(null)

const fetchData = () => {
  fetch('https://jsonplaceholder.typicode.com/posts/1')
    .then((response) => {
      if (!response.ok) {
        throw new Error('Network response was not ok')
      }
      return response.json()
    })
    .then((responseData) => {
      data.value = responseData
    })
    .catch((error) => {
      console.error('There has been a problem with your fetch operation:', error)
    })
}
</script>

<style></style>
```

## Events

Events in Vue are used to handle user interactions and trigger actions in the component. You can use the `v-on` directive or the shorthand `@` to listen for events.

`EventChildComponent.vue`:

```vue
<template>
  <div>
    <br />

    <button class="d-btn d-btn-error" @click="notifyParent">Click Me</button>
  </div>
</template>

<script setup>
const emit = defineEmits(['customEvent'])

function notifyParent() {
  emit('customEvent', 'Hello from child!')
}
</script>

<style></style>
```

`EventParentComponent.vue`:

```vue
<template>
  <div>
    <EventChildComponent @customEvent="handleCustomEvent" />
  </div>
</template>

<script setup>
import EventChildComponent from './EventChildComponent.vue'

function handleCustomEvent(message) {
  console.log('Received:', message)
  alert(message) // Shows: Hello from child!
}
</script>

<style></style>
```

Once clicked, the button in the child component will emit a custom event named `customEvent`, which the parent component listens for. When the event is triggered, the parent component's `handleCustomEvent` method is called, displaying an alert with the message passed from the child.

## Lifecycle Hooks

Lifecycle Hooks in Vue are special functions that allow you to run code at specific points in a component's lifecycle. They are useful for performing setup tasks, cleaning up resources, or reacting to changes in the component.

### Common Lifecycle Hooks

- `onMounted`: Called after the component is mounted to the DOM. This is a good place to perform initial data fetching or setup.
- `onUpdated`: Called after the component's reactive data has changed and the DOM has been updated. This is useful for reacting to changes in the component's data.
- `onUnmounted`: Called before the component is unmounted from the DOM. This is a good place to clean up resources, such as event listeners or timers.
- `onBeforeMount`: Called right before the component is mounted. This is useful for performing setup tasks that need to be done before the component is rendered.
- `onBeforeUpdate`: Called right before the component's reactive data changes and the DOM is updated. This is useful for performing tasks that need to be done before the component is re-rendered.
- `onBeforeUnmount`: Called right before the component is unmounted. This is useful for performing cleanup tasks that need to be done before the component is removed from the DOM.
- `onErrorCaptured`: Called when an error is thrown in a child component. This is useful for handling errors and preventing them from propagating to the parent component.
- `onActivated`: Called when a component is activated in a keep-alive component. This is useful for performing tasks when a component is reactivated.
- `onDeactivated`: Called when a component is deactivated in a keep-alive component. This is useful for performing tasks when a component is deactivated.

## Vue Router

Vue Router is the official router for Vue.js. It allows you to create single-page applications (SPAs) with navigation between different views or components.

It provides a way to define routes, navigate between them, and manage the state of the application.

### Basic Usage

To use Vue Router, you need to install it and configure it in your Vue application. You can define routes and map them to components.

```bash
npm install vue-router
```

Then, you can create a router instance and define your routes:

```javascript
import { createRouter, createWebHistory } from 'vue-router'

const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About },
]

const router = createRouter({
  history: createWebHistory(),
  routes,
})

export default router
```

## Layouts

### Grid

Vue.js allows you to create complex layouts using components and CSS frameworks like Tailwind CSS. You can use utility classes to style your components and create responsive designs.

The easiest way for more backend oriented `Software Writers` or `Developers` is to use the `grid` at first and then use the `flex` for more complex layouts.

The `grid` is a powerful layout system that allows you to create complex layouts with rows and columns. You can define the number of columns, their sizes, and how they should behave on different screen sizes.

The core concepts of the `grid` is to think about it as a container that can be always divided by 2. In other words: if you want to create a layout of 3 columns, small, medium, and large, you can use the `grid-cols-12` class and then use the `col-span` classes to define how many columns each element should span. The same applies to rows. For example:

- `col-span-2` for a small column
- `col-span-4` for a medium column
- `col-span-6` for a large column

Another hot trick is to use `sm:grid` to define the grid for small screens, rest will be handled by the `grid` classes automatically.

For example:

```html
<div class="grid sm:grid-cols-2 m-4 gap-4">
  <div class="min-h-[100px] rounded-lg bg-pink-300"></div>
  <div class="min-h-[100px] rounded-lg bg-blue-300"></div>
</div>
<div class="grid sm:grid-cols-12 m-4 gap-4">
  <div class="min-h-[100px] rounded-lg bg-violet-200 col-span-2"></div>
  <div class="min-h-[100px] rounded-lg bg-blue-400 col-span-10"></div>
</div>
<div class="grid sm:grid-cols-12 m-4 gap-4">
  <div class="min-h-[100px] rounded-lg bg-red-200 col-span-8">
    <div class="min-h-[50px] bg-amber-200"></div>
    <div class="min-h-[50px] bg-orange-300"></div>
  </div>
  <div class="min-h-[100px] rounded-lg bg-green-200 col-span-4"></div>
</div>
<div class="grid sm:grid-cols-12 m-4 gap-4">
  <div class="min-h-[200px] col-span-4 bg-red-200">
    <div class="min-h-[100px] bg-amber-200"></div>
    <div class="min-h-[100px] bg-orange-300"></div>
    <div class="min-h-[100px] bg-yellow-400"></div>
  </div>
  <div class="min-h-[200px] col-span-8 bg-green-200">
    <div class="grid grid-cols-3 h-full">
      <div class="bg-blue-200"></div>
      <div class="bg-purple-300"></div>
      <div class="bg-pink-400"></div>
    </div>
  </div>
</div>
```

### Flexbox

Flexbox is another powerful layout system that allows you to create flexible and responsive layouts. It is based on the concept of a flex container and flex items. The flex container is the parent element, and the flex items are the child elements.

The grid code below:

```html
<div class="grid sm:grid-cols-12 m-4 gap-4">
  <div class="min-h-[100px] rounded-lg bg-violet-200 col-span-2"></div>
  <div class="min-h-[100px] rounded-lg bg-blue-400 col-span-10"></div>
</div>
```

Can be easily converted to a flexbox layout like this:

```html
<div class="flex m-4 gap-4">
  <div class="min-h-[100px] rounded-lg bg-pink-300 flex-[2]"></div>
  <div class="min-h-[100px] rounded-lg bg-blue-300 flex-[10]"></div>
</div>
```

Or this:

```html
<div class="flex m-4 gap-4">
  <div class="min-h-[100px] rounded-lg bg-slate-400 w-1/6"></div>
  <div class="min-h-[100px] rounded-lg bg-blue-300 w-5/6"></div>
</div>
```

### Full-page / view-port scroll

In order to get for example 3 full-page sections that can be scrolled to, you can use the `snap` classes from Tailwind CSS. The `snap-y` class allows you to create a vertical snap scrolling effect, while the `snap-mandatory` class ensures that the scroll will snap to the nearest section.:

```html
<div class="h-screen snap-y snap-mandatory overflow-y-scroll scroll-smooth">
  <div class="h-screen flex items-center justify-center bg-base-200 snap-start">
    <br />
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam reprehenderit dolorum
      architecto atque consectetur quod porro maxime tenetur esse ipsum quisquam, maiores nobis
      temporibus sint modi ut inventore perferendis a quis deleniti quam eius rerum. Ullam,
      necessitatibus.
    </p>
  </div>
  <div class="h-screen flex items-center justify-center bg-slate-300 snap-start">
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam reprehenderit dolorum
      architecto atque consectetur quod porro maxime tenetur esse ipsum quisquam, maiores nobis
      temporibus sint modi ut inventore perferendis a quis deleniti quam eius rerum. Ullam,
      necessitatibus.
    </p>
  </div>
  <div class="h-screen flex items-center justify-center bg-base-400 snap-start">
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam reprehenderit dolorum
      architecto atque consectetur quod porro maxime tenetur esse ipsum quisquam, maiores nobis
      temporibus sint modi ut inventore perferendis a quis deleniti quam eius rerum. Ullam,
      necessitatibus.
    </p>
  </div>
</div>
```

This part was about re-learning me the core laws of layout design.

## Note

Sources:

- [Vue.js Documentation](https://vuejs.org/guide/introduction.html)
- [Vue.js Complete Course ( 2025 )](https://youtu.be/ymXJlPeM-qI?si=1jN6uMnxS2Ttyfj0)
- [Build any layout with Tailwind | Crash Course](https://youtu.be/rbSPe1tJowY?si=mKFUaJmQHuLj5Ho_)
