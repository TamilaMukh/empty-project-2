<template>
  <div>
    <div class="bg-black text-white py-16">
      <div class="container mx-auto">
        <div class="flex justify-between items-center">
          <div class="block">
            <h1 class="font-bold text-4xl mb-5">{{ movies[curID].title }}</h1>
            <div class="flex items-center border-t border-b border-gray-500 py-4">
              <div class="w-full">
                <h3 class="uppercase text-lg mb-4">Metascore</h3>
                <p class="w-2/3">Generally favorable reviews based on 68 Critic Reviews</p>
              </div>
              <p class="bg-green-500 font-bold text-xl p-3 rounded-xl text-white">{{ movies[curID].meta }}</p>
            </div>
            <div class="flex items-center border-b border-gray-500 py-4">
              <div class="w-full">
                <h3 class="uppercase text-lg mb-4">User Score</h3>
                <p class="w-2/3">Universal acclaim based on 1172 Ratings</p>
              </div>
              <p class="bg-green-500 font-bold text-xl p-3 rounded-xl text-white">{{ movies[curID].user }}</p>
            </div>
          </div>
          <video class="w-1/2" autoplay muted controls :src="movies[curID].video"></video>
        </div>
      </div>
    </div>
    <div class="container mx-auto">
      <div class="flex items-start">
        <div class="metascore w-1/3 mr-4">
          <h2 class="text-2xl border-b border-gray-300 py-2 mb-5">Critic reviews</h2>
          <div class="border-b border-gray-300 py-6" v-for="critic of movies[curID].metacritic" :key="critic.id">
            <div class="flex items-center mb-3">
              <p class="bg-green-500 font-bold text-xl p-3 rounded-xl text-white mr-3">{{ critic.rate }}</p>
              <div>
                <img :src="critic.img" alt="">
                <div class="flex items-center">
                  <p class="font-bold mr-3">{{ critic.name }}</p>
                  <p class="text-sm text-gray-500">{{ critic.date }}</p>
                </div>
              </div>
            </div>
            <p>{{ critic.review }}</p>
          </div>
        </div>
        <div class="userscore w-1/3">
          <h2 class="text-2xl border-b border-gray-300 py-2 mb-5">User reviews</h2>
          <div class="border-b border-gray-300 py-6" v-for="user of movies[curID].usercritic" :key="user.id">
            <div class="flex items-center mb-3">
              <p class="bg-green-500 font-bold text-xl p-3 rounded-xl text-white mr-3">{{ user.rate }}</p>
              <div>
                <img :src="user.img" alt="">
                <div class="block">
                  <p class="font-bold mr-3">{{ user.name }}</p>
                  <p class="text-sm text-gray-500">{{ user.date }}</p>
                </div>
              </div>
            </div>
            <p>{{ user.review }}</p>
          </div>
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
      curID: this.$route.params.id - 1,
      baseURL: 'http://localhost:3001/movies/',
      form: {
        name: "",
        review: "",
        date: "",
        rate: 0,
      },
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