<template>
  <section>
    <h2>{{title}}</h2>
      <ul>
        <li v-for="item in items" :key="item.id">
          <img :src="'https://image.tmdb.org/t/p/w185/' + item.poster_path" alt=""> <br>
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
          Voto: {{item.vote_average}} <br>
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

    };
  },
  methods: {

  }
};
</script>

<style lang="scss">
.flag{
  width: 50px;
}
</style>
