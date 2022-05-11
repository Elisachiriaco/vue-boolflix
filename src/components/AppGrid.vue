<template>
  <section>
    <h2>{{title}}</h2>
      <ul>
        <li v-for="item in items" :key="item.id">
          <img :src="'https://image.tmdb.org/t/p/w185/' + item.poster_path" alt=""> <br>
          Titolo: {{item.title ? item.title : item.name}} <br>
          Titolo originale: {{item.original_title ? item.original_title : item.original_name}}<br>
          Lingua: {{item.original_language}} <br>
          <!-- <img :src="require('../assets/' + item.original_language+'.jpg') " alt=""> -->
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

<style scoped lang="scss">

</style>
