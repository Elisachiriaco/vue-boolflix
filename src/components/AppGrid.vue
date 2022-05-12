<template>
  <section>
      <h2>{{title}}</h2>
      <ul>
        <li @mouseover="myshow" v-for="item in items" :key="item.id">
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
          <span v-for="(n,index) in 5" :key="index">
            <i :class="n <= transformStar ? 'fa-solid fa-star' : 'fa-regular fa-star' "></i>
          </span>
          <!-- <i v-for="(n,index) in star(item.vote_average)" :key="index" class="fa-solid fa-star"></i>
          <span v-if="item.vote_average === 0"><i class="fa-regular fa-star"></i>
          </span> <br> -->
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
    // star(number){
    //   return Math.round(number / 2);
    // },
  },
  computed:{
    transformStar(){
      return parseInt(this.vote_average / 2)
    }
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
    width: 100%;
    height: 280px;
    display: none;
    justify-content: center;
    padding: 20px 10px;
    background-color: rgba($color: black, $alpha: 0.9);
    overflow-y: auto;
}

.active{
  display: block;
}
</style>
