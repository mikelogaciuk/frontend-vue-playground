<script setup>
import HelloWorld from './components/HelloWorld.vue'
import AttributeBindingComponent from './components/AttributeBindingComponent.vue'
import ReactiveObjectsComponent from './components/ReactiveObjectsComponent.vue';
import ConditionalRenderingComponent from './components/ConditionalRenderingComponent.vue'
import StaticPropsComponent from './components/StaticPropsComponent.vue';
</script>

<template>
  <HelloWorld />
  <AttributeBindingComponent />
  <ReactiveObjectsComponent />
  <ConditionalRenderingComponent />
  <StaticPropsComponent name="John Doe" />
</template>

<style></style>
