<script setup>
import MovieContent from './components/MovieContent.vue'
</script>

<template>
  <div class="app-container">
    <Suspense>
      <MovieContent />
    </Suspense>
  </div>
</template>

<style scoped>
.app-container {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-image: linear-gradient(to right, #88cda5, #07b4e2);
  background-size: cover;
}
</style>
