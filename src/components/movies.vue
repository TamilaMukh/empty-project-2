<template>
  <div class="container mx-auto">
    <div
      class="py-8 border-b border-gray-500" v-for="movie of allPosts" :key="movie.id">
      <div
        @click="$router.push({ name: 'movie', params: { id: movie.id } })"
        class="flex justify-between items-start">
        <img class="mr-3" :src="movie.image" alt="" />
        <div class="info w-full">
          <h2 class="font-bold text-xl">{{ movie.id }}. {{ movie.title }}</h2>
          <p class="my-2 text-gray-500">{{ movie.date }}</p>
          <p>{{ movie.desc }}</p>
        </div>
        <p class="bg-green-500 font-bold text-xl p-3 rounded-xl text-white">
          {{ movie.meta }}
        </p>
      </div>
    </div>
    <form class="block my-10" action="">
      <p class="text-xl font-bold">Enter title:</p>
      <input
        class="block my-3 border border-gray-300 w-full p-3 rounded-xl"
        type="text"
        v-model="form.title"
        placeholder="Enter title..."
      />
      <p class="text-xl font-bold">Enter date:</p>
      <input
        class="block my-3 border border-gray-300 w-full p-3 rounded-xl"
        type="text"
        v-model="form.date"
        placeholder="Enter date..."
      />
      <p class="text-xl font-bold">Enter description:</p>
      <input
        class="block my-3 border border-gray-300 w-full p-3 rounded-xl"
        type="text"
        v-model="form.desc"
        placeholder="Enter desc..."
      />
      <p class="text-xl font-bold">Enter image:</p>
      <input
        class="block my-3 border border-gray-300 w-full p-3 rounded-xl"
        type="text"
        v-model="form.image"
        placeholder="Enter image..."
      />
      <p class="text-xl font-bold">Enter video:</p>
      <input
        class="block my-3 border border-gray-300 w-full p-3 rounded-xl"
        type="text"
        v-model="form.video"
        placeholder="Enter video..."
      />
      <p class="text-xl font-bold">Enter genre:</p>
      <input
        class="block my-3 border border-gray-300 w-full p-3 rounded-xl"
        type="text"
        v-model="form.genre"
        placeholder="Enter genre..."
      />
      <p class="text-xl font-bold">Enter metascore:</p>
      <input
        class="block my-3 border border-gray-300 w-full p-3 rounded-xl"
        type="number"
        v-model="form.meta"
        placeholder="Enter meta..."
      />
      <p class="text-xl font-bold">Enter userscore:</p>
      <input
        class="block my-3 border border-gray-300 w-full p-3 rounded-xl"
        type="number"
        v-model="form.user"
        placeholder="Enter user..."
      />
      <button
        class="
          bg-green-400
          px-20
          py-4
          text-white
          mx-auto
          block
          rounded-xl
          font-bold
          text-2xl
        "
        @click="addMovie()"
      >
        Commit Movie
      </button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
import { mapActions, mapGetters } from "vuex";

export default {
  data() {
    return {
      baseURL: "http://localhost:3001/movies",
      form: {
        title: "",
        date: "",
        desc: "",
        image: "",
        video: "",
        meta: 0,
        user: 0,
        genre: "",
      },
    };
  },
  computed: mapGetters(["allPosts"]),
  async mounted() {
    this.fetchPosts();
  },
  methods: {
    ...mapActions(["fetchPosts"]),
    async addMovie() {
      try {
        const res = await axios.post(this.baseURL, {
          title: this.form.title,
          date: this.form.date,
          desc: this.form.desc,
          image: this.form.image,
          video: this.form.video,
          meta: this.form.meta,
          user: this.form.user,
          genre: this.form.genre,
        });
        this.movies = [...this.movies, res.data];
      } catch (e) {
        console.error(e);
      }
    },
  },
};
</script>