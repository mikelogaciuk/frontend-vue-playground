<script setup>
import HelloWorld from './components/HelloWorld.vue'
import AttributeBindingComponent from './components/AttributeBindingComponent.vue'
import ReactiveObjectsComponent from './components/ReactiveObjectsComponent.vue';
import ConditionalRenderingComponent from './components/ConditionalRenderingComponent.vue'
import StaticPropsComponent from './components/StaticPropsComponent.vue';
import DynamicPropsLoaderComponent from './components/DynamicPropsLoaderComponent.vue';
import SlotComponent from './components/SlotComponent.vue';
import FallbackDefaultComponent from './components/FallbackDefaultComponent.vue';
import NamedSlotComponent from './components/NamedSlotComponent.vue';
import ProvideAndInjectComponent from './components/ProvideAndInjectComponent.vue';
import WatcherComponent from './components/WatcherComponent.vue';
import TemplateRefComponent from './components/TemplateRefComponent.vue';
import DataFetchComponent from './components/DataFetchComponent.vue';
import EventParentComponent from './components/EventParentComponent.vue';
import LayoutComponent from './components/LayoutComponent.vue';
</script>

<template>
  <HelloWorld />
  <AttributeBindingComponent />
  <ReactiveObjectsComponent />
  <ConditionalRenderingComponent />
  <StaticPropsComponent name="John Doe" />
  <DynamicPropsLoaderComponent />
  <SlotComponent>
    <p>This is content passed to the slot.</p>
  </SlotComponent>
  <FallbackDefaultComponent> </FallbackDefaultComponent>
  <FallbackDefaultComponent>
    <h1>Custom Fallback Content using Fallback Component</h1>
  </FallbackDefaultComponent>
  <NamedSlotComponent>
    <template #upper>
      <h1>Upper Slot Content</h1>
    </template>
    <template #lower>
      <h2>Lower Slot Content</h2>
    </template>
  </NamedSlotComponent>
  <ProvideAndInjectComponent />
  <WatcherComponent />
  <TemplateRefComponent />
  <DataFetchComponent />
  <EventParentComponent />
  <LayoutComponent />
</template>

<style></style>
