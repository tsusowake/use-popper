<template>
  <NuxtLink to="/">Home</NuxtLink>
  <NuxtLink to="/sample">Sample</NuxtLink>
  <NuxtPage />
</template>

<script setup lang="ts">
const route = useRoute();
</script>

<style lang="scss">
body {
  margin: 0;
  width: 1080px;
  overflow: scroll;
}
</style>
