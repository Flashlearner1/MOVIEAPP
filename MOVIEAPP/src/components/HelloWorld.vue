<script setup>
import { ref } from 'vue';


const input_content = ref ('');
const movies = ref ([]);
import env from '@/env.js'


const getmovies =() =>{

  fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${input_content.value}`)
  .then(response => response.json())
  .then(data => movies.value = data)

  return{
    movies
  }
}

</script>


<template>
<div class="Container">
  <div class="main-container">
    <h2>Imdb Movies</h2>
    <div class="box">
      <form @submit.prevent="getmovies">
        <input type="text" placeholder="Search Omdb movies" v-model="input_content">
        <button @click="getmovies">Search</button>
        <h3>Results</h3>
      </form>
    </div>
  </div>

  <div class="movielist">
    <div class="img">
      <ul>
        
        <li v-for="movies in movies">
          
          {{ movies }}

          
        </li>
      </ul>
    </div>
  </div>
</div>
</template>


