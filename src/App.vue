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

</style>
