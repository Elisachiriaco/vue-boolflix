<template>
  <div id="app">
    <header>
      <app-search @performSearch="search"/>
    </header>
    <main>
      <app-loader v-if="loading"/>
      <app-grid :items="movies" title="Movies" :loader="loading"/>
      <app-loader v-if="loadingSeries"/>
      <app-grid :items="series" title="Series" :loader="loadingSeries"/>
    </main>
  </div>
</template>

<script>
import axios from 'axios';
import AppLoader from './components/AppLoader.vue'
import AppSearch from './components/AppSearch.vue';
import AppGrid from './components/AppGrid.vue';

export default {
  name: 'App',
  components: {
    AppLoader,
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

header{
  height: 60px;
  background-color: $bg-header;
  h1{
    color: $color-title;
  }
}

main{
  background-color: $bg-main;
  h2{
    padding-left: 20px;
    color: $bg-header;
    font-weight: 400;
    font-style: italic;
  }
}
</style>
