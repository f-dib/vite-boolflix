<script>
import axios from 'axios';

import {store} from '../store.js';

export default {
    name: 'AppHeader',

    data(){
        return {
            store
        }
    },
    methods: {
        handleSearchInput() {
            
            this.$emit('search');

            
            if (this.store.searchText.trim() === '') {
                this.getDefaultMovies();
            }
        },
        clearSearchInput() {
        
            this.store.searchText = '';
            this.$emit('search');
            },
            getDefaultMovies() {
            axios.get('https://api.themoviedb.org/3/movie/popular?language=it-IT&page=1&api_key=e99307154c6dfb0b4750f6603256716d').then((res) => {
                
                this.store.popularFilm = res.data.results;
                console.log(this.store.popularFilm);

                axios.get('https://api.themoviedb.org/3/tv/popular?language=it-IT&page=1&api_key=e99307154c6dfb0b4750f6603256716d').then((res2) => {
                this.store.popularSeries = res2.data.results;
                console.log(this.store.popularSeries);
                
                })
            })
            .catch((err) => {
            console.log(err);
            });
        } 
    }
}
</script>

<template>
    <nav class="navbar bg-black mb-5 position-fixed top-0 start-0 w-100">
        <div class="container-fluid">
            <a class="navbar-brand"><img class="img-fluid-logo" src="/public/img/logo.png" alt=""></a>
            <div class="d-flex">
                <div class="my_avatar me-4"><img class="img-fluid" src="/public/img/Netflix-avatar.png" alt=""></div>
                <div class="d-flex" role="search">
                    <input class="form-control me-1 bg-black text-white" type="search" placeholder="Search" aria-label="Search" v-model="store.searchText" @keyup.enter="$emit('search')" @keyup="handleSearchInput">
                    <button @click="$emit('search')" class="btn text-white" type="submit"><i class="fa-solid fa-magnifying-glass"></i></button>
                </div>
            </div>
        </div>
    </nav>
</template>

<style lang="scss">
    .navbar {
        z-index: 12;

        .img-fluid-logo {
        height: 50px!important;
        }

        .my_avatar{
            width: 40px;
            height: 40px;
        }
    }

</style>