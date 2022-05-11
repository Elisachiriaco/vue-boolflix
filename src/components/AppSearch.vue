<template>
    <div class="container">
        <div class="row align-items-center">
            <div class="col-6">
                  <h1>Boolflix</h1>
            </div>
            <div class="col-6 justify-content-end">
                <input type="text" v-model="search" @keyup.enter="$emit('performSearch', search)">
                <button @click="cerca">Cerca</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'AppSearch',
    data(){
        return{
            search: '',
        }
    },
    methods: {
        cerca(){
            this.$emit('performSearch',this.search);
            this.search = ''
        }
    }
}
</script>

<style lang="scss">

</style>
