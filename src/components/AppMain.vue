<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-6">
        <div class="input-group mb-3">
          <input type="text" class="form-control" placeholder="Cerca un film" aria-label="Cerca un film" aria-describedby="basic-addon2" v-model="inputText"  @keyup.enter="getSearch"/>
          <div class="input-group-append">
            <button type="button" class="btn btn-outline-success" @click="getSearch">
              Search 
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="row justify-content-center">
      <div class="col-6">
        <ul v-for="(movie, index) in listMovie" :key="index">
          <li>Titolo: {{movie.title}}</li>
          <li>Titolo originale: {{movie.original_title}}</li>
          <li>Lingua: {{movie.original_language}}</li>
          <li>Voto: {{movie.vote_average}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "AppMain",
  data() {
    return {
      apiURL: "https://api.themoviedb.org/3/search/movie",
      apiKey: "?api_key=f406d2834d20f06f97a5f2d346598f37",
      inputText: "",
      apiLang: "language=it-IT",
      listMovie: [],
    };
  },
  methods: {
    getSearch() {
      axios.get(this.apiURL + this.apiKey + "&query=" + this.inputText + "&" + this.apiLang).then((res) => {
          this.listMovie = res.data.results;
          console.log(this.listMovie)
        })
        .catch((error) => {
          console.log(error);
        });
        this.inputText =""
    },
  },
};
</script>

<style scoped lang="scss">

</style>
