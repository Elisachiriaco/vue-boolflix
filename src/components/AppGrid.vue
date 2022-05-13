<template>
  <section>
      <h2>{{title}}</h2>
      <ul>
        <li class="noresult" v-if="items.length === 0">Non ci sono risultati per questa ricerca</li>
        <li @mouseenter="myshow" @mouseleave="noshow" v-for="item in items" :key="item.id">
          <img :src="item.poster_path ? 'https://image.tmdb.org/t/p/w342/' + item.poster_path : require('../assets/netflix.png')" alt=""> <br>
          <div class="showinfo" :class="show ? 'active' : '' ">
          Titolo: {{item.title ? item.title : item.name}} <br>
          Titolo originale: {{item.original_title ? item.original_title : item.original_name}}<br>
          <div v-if="item.original_language === 'it'">
           <span>Lingua:</span> <img class="flag" :src="require('../assets/it.jpg')"  alt="">
          </div>
          <div v-else-if="item.original_language === 'en'">
          <span>Lingua: </span><img class="flag" :src="require('../assets/en.jpg')"  alt="">
          </div>
          <div v-else>
          Lingua: {{item.original_language}}
          </div>
          Voto: 
          <i v-for="(n,index) in star(item.vote_average)" :key="index" class="fa-solid fa-star"></i>
          <span v-if="item.vote_average === 0"><i class="fa-regular fa-star"></i>
          </span> <br>
          Trama: {{item.overview}}
          </div>
        </li>
      </ul>
  </section>
</template>

<script>

export default {
  name: "AppMain",
  props:{
        items: Array,
        loader: Boolean,
        title: String
    },
  data() {
    return {
      show: false,
    };
  },
  methods: {
    myshow(){
      return this.show = true 
    },
    noshow(){
      return this.show = false 
    },
    star(number){
      return Math.round(number / 2);
    },
  },
};
</script>

<style lang="scss">
ul{
    color: white;
    width: 100%;
    height: 400px;
    display: flex;
    flex-flow: row nowrap;
    list-style-type: none;
    overflow-x:auto;
      li{
        position: relative;
        width: 35%;
        margin: 15px;
    }    
    img{
      width: 200px;
      border-radius: 10px;
    }
}
.flag{
    width: 20px;
    height: 20px;
}   
img{
  height:280px;
}

.showinfo{
    position: absolute;
    top: 0;
    left: 0;
    width: 200px;
    height: 280px;
    display: none;
    justify-content: center;
    padding: 20px 10px;
    background-color: rgba($color: black, $alpha: 0.9);
    overflow-y: auto;
    border-radius: 10px;
}

.active{
  display: block;
}

.noresult{
  color: black;
  font-style: italic;
}
// scrollbar
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-track {
  background: #B5B5B5; 
}
 
::-webkit-scrollbar-thumb {
  background: #888; 
}

::-webkit-scrollbar-thumb:hover {
  background: #555; 
}
</style>
