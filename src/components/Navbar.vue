<template> 
  <div class="bg-black text-white py-5"> 
      <div class="container mx-auto"> 
        <div class="flex items-center justify-between" v-for="user of users" :key="user.id"> 
            <div class="flex w-1/3"> 
                <img class="w-10" src="https://www.metacritic.com/images/icons/metacritic-icon.svg" alt=""> 
                <img class="w-20" src="https://www.metacritic.com/images/icons/metacritic-wordmark.svg" alt=""> 
            </div> 
            <div class="w-1/3 px-5"> 
                <input class="w-full bg-black text-white border-2 border-gray-300 rounded-lg p-2" placeholder="Search..." type="text"> 
            </div> 
            <div class="flex justify-between items-center w-1/3 font-bold"> 
                <router-link to="/">Games</router-link> 
                <router-link to="/">Movies</router-link> 
                <router-link to="/">TV</router-link> 
                <router-link to="/">Music</router-link> 
                <router-link v-if="status == false" class="border-2 border-white p-2 rounded-lg" to="/">Sign in</router-link> 
                 <p @click="status = false" v-if="status == true" class="border-2 border-white p-2 rounded-lg">logout</p>  
                <div v-if="status == true"><h1 @mouseenter="dopinfa = true" class="text-white text-right">{{ user.name }} {{ user.surname }} <br> <span>GPA:</span> {{ user.gpa }}</h1></div>
                <div v-if="dopinfa == true" class="ml-2 text-right"><h1>{{ user.middlename }} <br> {{ user.email }}</h1></div>
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
      users: [],
      baseURL: 'http://localhost:3001/users/',
      status: true,
      dopinfa: false
    };
  },
  async created() {
    try {
      const res = await axios.get(this.baseURL);
      this.users = res.data;
    } catch (e) {
      console.error(e);
    }
  },
};
</script>