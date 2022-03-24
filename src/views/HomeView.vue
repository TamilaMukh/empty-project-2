<template>
  <div class="home">
    <movies />
  </div>
</template>

<script>
import movies from '@/components/movies.vue'
export default {
  name: 'HomeView',
  components: {
    movies
  }
}
</script>
