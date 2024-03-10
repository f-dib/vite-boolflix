<script>
import axios from 'axios';
import {store} from './store.js';

import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';

export default {

    data(){
      return {
        store,
        isLoading: true
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
    });

    axios.get('https://api.themoviedb.org/3/genre/movie/list?language=it&api_key=e99307154c6dfb0b4750f6603256716d').then(res3 => {
        this.store.genre = res3.data.genres

        axios.get('https://api.themoviedb.org/3/genre/tv/list?language=it&api_key=e99307154c6dfb0b4750f6603256716d').then(res4 => {
            this.store.totalGenre = this.store.genre.concat(res4.data.genres)
            console.log(this.store.totalGenre)
        })
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
    },
    mounted() {

      setTimeout(() => {
          this.isLoading = false;
        }, 2000);

    }
}
</script>

<template>
    <div id="splash-page" v-if="isLoading">
        <div class="d-flex flex-column justify-content-center align-items-center h-100">
            <img class="pb-5" src="../public/img/logo.png" alt="">
            <div class="spinner-border my_color mt-5" role="status">
              <span class="visually-hidden">Loading...</span>
            </div>
        </div>
    </div> 

    <div v-else class="my_page">
      <AppHeader @search="searchFilm()"></AppHeader>
      <AppMain></AppMain>
    </div>
</template>

<style lang="scss">
    #splash-page{
      width: 100vw;
      height: 100vh;

      color: #dc1a28;
      background-color: black;

      .my_color{
        color: #dc1a28 !important;
      }
    }

    .my_page{
        padding-top: 120px;
        background-color: black;
    }
</style>
