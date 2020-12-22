<template>
  <div id="app" class="h-screen bg-gray-100 ">
    <!-- 
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div> 
    -->
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/Goal">Goal</router-link>
    </nav>
    <router-view class=""/>
    <!-- col-start-1 col-end-10 sm:col-start-2  sm:col-end-9 shadow-lg rounded-lg -->
  </div>
</template>

<script>
import './assets/styles/styles.css'
export default {
  
}
</script>

<style>

</style>
