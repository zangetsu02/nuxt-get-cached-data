<script setup lang="ts">


</script>

<template>
  <div>
    <h1>Index page</h1>

    <div v-for="index in 10" :key="index">
      <Test/>
    </div>

    <NuxtLink to="/about">To the about page</NuxtLink>
  </div>
</template>
