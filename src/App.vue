<template>
  <div id="app">
    <navbar />
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<script> 
import navbar from '@/components/Navbar.vue' 

export default { 
  components: { 
    navbar 
  } 
} 
</script>