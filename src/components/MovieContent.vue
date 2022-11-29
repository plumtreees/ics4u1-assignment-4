<script setup>
import { ref } from "vue";
import axios from "axios";

const movie = ref(false);
const id = ref("");

const trailer = ref("");
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
  trailer.value = movie.value.videos.results.filter((trailer) => trailer.type === "Trailer").at(0).key;
  runtime.value = `${Math.floor(movie.value.runtime / 60)}h${(movie.value.runtime % 60)}m`;
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
  <div class="background-image" :style="{ backgroundImage: `url(https://image.tmdb.org/t/p/original${movie.backdrop_path})` }"></div>
  <div class="foreground">
    <div class="movie-content" v-if="movie">
      <img id="poster" :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path">
      <h1>{{ movie.title }}</h1>
      <h2>{{ movie.release_date }} • {{ movie.spoken_languages.at(0).english_name }} • {{ movie.genres.at(0).name }} •
        {{ runtime }}</h2>
      <iframe id="trailer" :src="`https://www.youtube.com/embed/${trailer}`"></iframe>
      <h3>{{ movie.tagline }}</h3>
      <p id="overview">{{ movie.overview }}</p>
    </div>
  </div>
</template>

<style scoped>
  .list-container {
  width: 100vw;
  padding: 1rem;
  z-index: 2;
  background-color: #032541;
  border: 4px solid transparent;
  border-image: linear-gradient(to right, #88cda5, #07b4e2) 10;
}

.list-container label {
  color: white;
}

.list-container select {
  border-radius: 8px;
  margin: 10px 0;
}

#get {
  padding: 0 1rem;
  border-radius: 8px;
  border-color: #767676;
}

.background-image {
  position: fixed;
  left: 0;
  right: 0;
  z-index: 1;
  width: 100%;
  height: 100%;
  filter: blur(8px);
  -webkit-filter: blur(8px);
  background-position: center;
  background-size: cover;
}

.foreground {
  display: grid;
  width: 100%;
  height: 100%;
  z-index: 2;
  background-color: #000000b4;
}

.movie-content {
  display: grid;
  width: 80vw;
  grid-template-columns: repeat(16, 4%);
  gap: 0.5rem 2rem;
  justify-self: center;
  align-self: center;
  color: white;
  text-shadow: 0 0 0.7rem #000000d7;
}

#poster {
  width: 100%;
  grid-column: span 4;
  grid-row: 1 / span 6;
  aspect-ratio: 2 / 3;
  border-radius: 8px;
  color: #000;
  box-shadow: 0 0 1rem 3px #000000b4;
}

#trailer {
  width: 100%;
  grid-column: 11 / span 6;
  grid-row: span 2;
  aspect-ratio: 16 / 9;
  border-radius: 8px;
  border: none;
  box-shadow: 0 0 1rem 3px #000000b4;
}

h1 {
  grid-column: 5 / span 10;
  vertical-align: middle;
  font-size: 3vw;
}

h2 {
  grid-column: span 6;
  font-variant: small-caps;
  font-weight: normal;
}

h3 {
  grid-column: span 6;
  font-weight: normal;
  font-style: italic;
  position: relative;
  bottom: 10%;
}

#overview {
  grid-column: span 6;
  grid-row: 4 / span 4;
  position: relative;
  bottom: 10%;
}
</style>
