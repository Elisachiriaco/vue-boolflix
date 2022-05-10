<template>
  <div id="app">
    <app-main />
  </div>
</template>

<script>
import AppMain from './components/AppMain.vue'

export default {
  name: 'App',
  components: {
    AppMain
  }
}
</script>

<style lang="scss">
@import "./style/general.scss";
@import "./style/vars.scss";
</style>
