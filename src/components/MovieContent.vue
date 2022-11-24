<script setup>
import { ref } from "vue";
import axios from "axios";

const movie = ref(false);
const id = ref("");

const trailers = ref("");
const runtime = ref("");

const getMovie = async () => {
  movie.value = (
    await axios.get(`https://api.themoviedb.org/3/movie/${id.value}`, {
      params: {
        api_key: "82ec5f2e2891c6f52b2ebda2cc0aa8a6",
        append_to_response: "videos",
      },
    })
  ).data;
  trailers.value = movie.videos.results.filter((trailer) => trailer.type === "Trailer");
  runtime.value = Math.floor(movie.runtime / 100) + "h" + (movie.runtime % 100) + "m";
  console.log(movie);
};
</script>

<template>
  <div class="list-container">
    <label for="movies-list">Choose a movie to view its information:</label><br>
    <select id="movies-list" v-model="id">
      <option value="0" disabled>Choose a movie</option>
      <option value="11216">Cinema Paradiso</option>
      <option value="13">Forrest Gump</option>
      <option value="483855">Papers, Please: The Short Film</option>
      <option value="496243">Parasite</option>
      <option value="447404">Pokémon Detective Pikachu</option>
      <option value="2062">Ratatouille</option>
      <option value="324857">Spider-Man: Into the Spider-Verse</option>
      <option value="129">Spirited Away</option>
      <option value="1402">The Pursuit of Happyness</option>
      <option value="372058">Your Name</option>
    </select>
    <button id="get" @click="getMovie()">Get</button>
  </div>
  <p>{{ runtime }}</p>
  <p>{{ id }}</p>
  <p v-if="movie">clicked</p>
  <div class="movie-content" v-if="movie">
    <h1>{{ movie.title }}</h1>
    <h2>{{ movie.release_date }} • {{ movie.spoken_languages.at(0).english_name }} • {{ movie.genres.at(0).name }} • {{runtime}}</h2>
    <h3>{{ movie.tagline }}</h3>
    <p>{{ movie.overview }}</p>
    <img :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path" id="poster">
    <iframe :src="'https://www.youtube.com/embed/' + movie.videos.results.at(0).key" id="trailer"></iframe>
  </div>
</template>

<style scoped>

</style>
