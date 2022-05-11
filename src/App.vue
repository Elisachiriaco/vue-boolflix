<template>
  <div id="app">
    <header>
      <h1>Boolflix</h1>
      <app-search @performSearch="search"/>
    </header>
    <main>
      <app-grid :items="movies" title="Movies" :loader="loading"/>
      <app-grid :items="series" title="Series" :loader="loadingSeries"/>
    </main>
  </div>
</template>

<script>
import axios from 'axios';
import AppSearch from './components/AppSearch.vue';
import AppGrid from './components/AppGrid.vue';

export default {
  name: 'App',
  components: {
    AppSearch,
    AppGrid
  },
  data(){
    return{
      apiKey: "f406d2834d20f06f97a5f2d346598f37",
      apiURL: "https://api.themoviedb.org/3/search/",
      movies: [],
      series: [],
      loading: false,
      loadingSeries: false 
    }
  },
    methods:{
    getMovies(queryParams){
      axios.get(this.apiURL + 'movie', queryParams).then((res)=>{
        // console.log(res.data.results)
        this.movies = res.data.results;
        this.loading = false;
      }).catch((error)=>{
        console.log(error);
      })
    },
    getSeries(queryParams){
      axios.get(this.apiURL + 'tv', queryParams).then((res)=>{
        //console.log(res.data.results)
        this.series = res.data.results;
        this.loadingSeries = false;
      }).catch((error)=>{
        console.log(error);
      })
    },
    search(text){
       const queryParams = {
        params:{
          api_key: this.apiKey,
          query: text
        }
      }
      this.loading = true;
      this.loadingSeries = true;
      this.getMovies(queryParams);
      this.getSeries(queryParams);
    }
  }
}
</script>

<style lang="scss">
@import "./style/general.scss";
@import "./style/vars.scss";

</style>
