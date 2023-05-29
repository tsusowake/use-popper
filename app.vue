<template>
  <NuxtLink to="/">Home</NuxtLink>

  <div class="page-container">
    <NuxtPage />
  </div>
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

.page-container {
  background-color: #aaa;
}
</style>
