<script>
import {store} from '../store.js';

export default {
    name: 'AppFilm',

    data(){
        return {
            store
        }
    },
    methods: {
        movieImg(currentElement){
            return `https://image.tmdb.org/t/p/w342${currentElement}`;
        },
        movieFlag(currentElement){
                return `https://flagcdn.com/16x12/${currentElement}.png`;
        },
        rating(currentElement){
            let ratingStar = Math.round(currentElement / 2);
            let emptyStar = Array(5).fill('fa-solid fa-star');
            
            // Use v-bind:class instead of modifying the style directly
            return emptyStar.map((starClass, index) => ({
                class: {
                [starClass]: index < ratingStar, // Apply class based on filled stars
                'text-danger': index < ratingStar, // Apply color for filled stars
                },
            }));
        }
    }
}
</script>

<template>
    <h2 class="ms-2 mb-3">FILM</h2>
    <div class="d-flex flex-wrap mb-5">
        <div class="my_grid m-auto" v-for="currentElement in store.popularFilm">
            <img class="my_img-fluid" :src="movieImg(currentElement.poster_path)" alt="">
            <div>{{ currentElement.title }}</div>
            <div><img :src="movieFlag(currentElement.original_language)" alt=""></div>
            <div><i v-for="(star, index) in rating(currentElement.vote_average)" :key="index"><i v-bind:class="star.class"></i></i></div>
        </div>
    </div>
</template>

<style lang="scss">

</style>