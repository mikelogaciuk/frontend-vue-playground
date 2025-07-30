<template>
  <br />
  <!-- Grid layout part -->
  <h1 class="text-2xl m-4">Below there is a grid layout stuff...</h1>
  <br />
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


  <!-- Flex box part -->
  <h1 class="text-2xl m-4">Below there is a flex box layout stuff...</h1>
  <br />
  <div class="flex m-4 gap-4">
    <div class="min-h-[100px] rounded-lg bg-pink-300 flex-1"></div>
    <div class="min-h-[100px] rounded-lg bg-blue-300 flex-1"></div>
  </div>
  <div class="flex m-4 gap-4">
    <div class="min-h-[100px] rounded-lg bg-blue-200 flex-[2]"></div>
    <div class="min-h-[100px] rounded-lg bg-pink-300 flex-[10]"></div>
  </div>
  <div class="flex m-4 gap-4">
    <div class="min-h-[100px] rounded-lg bg-slate-400 w-1/6"></div>
    <div class="min-h-[100px] rounded-lg bg-blue-300 w-5/6"></div>
  </div>
  <div class="flex m-4 gap-4">
    <div class="min-h-[150px] rounded-lg bg-red-400 w-7/12"></div>
    <div class="min-h-[150px] rounded-lg bg-green-400 w-5/12">
      <div class="flex flex-col h-full">
        <div class="min-h-[50px] bg-blue-200"></div>
        <div class="min-h-[50px] bg-purple-300"></div>
        <div class="min-h-[50px] bg-pink-400"></div>
      </div>
    </div>
  </div>
</template>

<script setup>

</script>

<style></style>
