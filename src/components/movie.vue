<template>
  <div>
    <div class="bg-black text-white py-16">
      <div class="container mx-auto">
        <div class="flex justify-between items-center">
          <div class="block">
            <h1 class="font-bold text-4xl mb-5">{{ movies[singleRoma].title }}</h1>
            <div class="flex items-center border-t border-b border-gray-500 py-4">
              <div class="w-full">
                <h3 class="uppercase text-lg mb-4">Metascore</h3>
                <p class="w-2/3">Generally favorable reviews based on 68 Critic Reviews</p>
              </div>
              <p class="bg-green-500 font-bold text-xl p-3 rounded-xl text-white">{{ movies[singleRoma].meta }}</p>
            </div>
            <div class="flex items-center border-b border-gray-500 py-4">
              <div class="w-full">
                <h3 class="uppercase text-lg mb-4">User Score</h3>
                <p class="w-2/3">Universal acclaim based on 1172 Ratings</p>
              </div>
              <p class="bg-green-500 font-bold text-xl p-3 rounded-xl text-white">{{ movies[singleRoma].user }}</p>
            </div>
          </div>
          <video class="w-1/2" autoplay muted controls :src="movies[singleRoma].video"></video>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      movies: [],
      singleRoma: this.$route.params.id - 1,
    };
  },
  async created() {
    try {
      const res = await axios.get(`http://localhost:3001/movies`);
      this.movies = res.data;
    } catch (e) {
      console.error(e);
    }
  },
};
</script>