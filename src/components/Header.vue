<script>
import { ref } from "vue";
// const list = ref("");
const moviesList = ; //left off herer
const clicked = ref(false);
const 

const getMovie = () => {
  clicked.value = true;

}
</script>

<template>
  <div class="list-container">
    <label for="movies-list">Choose a movie to view its information:</label><br>
    <select id="movies-list" >
      <option value="" selected>--Choose a movie--</option>
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
  <div v-if="clicked" class="print-id">
    <p>{{ list }}</p>
  </div>
</template>

<style scoped>

</style>