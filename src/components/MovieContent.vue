<script setup>
import { ref } from "vue";
import axios from "axios";

const movie = ref();
const clicked = ref(false);
const id = ref("");

const trailers = ref("");
const runtime = ref("");

const getMovie = () => {
  movie = axios.get(`https://api.themoviedb.org/3/movie/${id.value}`, {
    params: {
      api_key: "82ec5f2e2891c6f52b2ebda2cc0aa8a6",
      append_to_response: "videos",
    }
  }).then((movie) => {
    clicked.value = true;
    console.log(clicked.value);
    console.log(movie.data);
    // trailers = movie.data.videos.results.filter((trailer) => trailer.type === "Trailer");
    // runtime = Math.floor(movie.data.runtime / 100) + "h" + movie.data.runtime % 100 + "m";
  });
}
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
  <p>{{clicked}}</p>
  <p>{{ id }}</p>
  <p v-if="clicked">clicked</p>
  <div class="movie-content" v-if="clicked">
    <h1>{{ movie.data.title }}</h1>
    <h2>{{ movie.data.release_date }}</h2>
    <!--  • {{ movie.data.spoken_languages.at(0).english_name }} •
      {{ movie.data.genres.at(0).name }} -->
    <h3>{{ movie.data.tagline }}</h3>
    <p>{{ movie.data.overview }}</p>
  </div>
</template>

<style scoped>

</style>
