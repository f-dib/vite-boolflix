<script>
import axios from 'axios';
import {store} from './store.js';

import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';

export default {

    data(){
      return {
        store
      }
    },
    created() {
      axios.get('https://api.themoviedb.org/3/movie/popular?language=it-IT&page=1&api_key=e99307154c6dfb0b4750f6603256716d').then(res => {

        this.store.popularFilm = res.data.results
        console.log(this.store.popularFilm)

        axios.get('https://api.themoviedb.org/3/tv/popular?language=it-IT&page=1&api_key=e99307154c6dfb0b4750f6603256716d').then(res2 => {
        
          this.store.popularSeries = res2.data.results
          console.log(this.store.popularSeries)
          
        })
    }).catch(err => {
      console.log(err)
    })
    },
    components: {
      AppHeader,
      AppMain
    },
    methods: {
      searchFilm(){
        
        axios.get('https://api.themoviedb.org/3/search/movie?language=it-IT&api_key=e99307154c6dfb0b4750f6603256716d&query=' + this.store.searchText).then(res => {

            this.store.popularFilm = res.data.results
            
            axios.get('https://api.themoviedb.org/3/search/tv?language=it-IT&api_key=e99307154c6dfb0b4750f6603256716d&query=' + this.store.searchText).then(res2 => {
        
              this.store.popularSeries = res2.data.results
      
            })
        })
      }
    }
}
</script>

<template>
    <AppHeader @search="searchFilm()"></AppHeader>
    <AppMain></AppMain>
</template>

<style lang="scss">

</style>
