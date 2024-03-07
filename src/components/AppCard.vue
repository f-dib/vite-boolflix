<script>
import {store} from '../store.js';

export default {
    name: 'AppCard',

    props: {
        card: Object,
    },

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

            let flag = currentElement

            switch(currentElement){
            case "ja":
                flag = "jp";
                break;
            case "en":
                flag = "us";
                break;
            case "ko":
                flag = "kr";
                break;
            case "da":
                flag = "dk";
                break;
            case "zh":
                flag = "cn";
                break;
            case "uk":
                flag = "gb"
                break;
            default:
            }
            return `https://flagcdn.com/16x12/${flag}.png`;

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
    <div class="my_grid p-0 position-relative col-3 m-1">
        <img class="my_img-fluid" :src="movieImg(card.poster_path)" alt="">
        
        <div class="position-absolute my_overlay text-white p-2 d-flex flex-column justify-content-center">
            <div><span class="pe-2 fw-bold">Titolo:</span> {{ card.title ? card.title : card.name }} </div>
            <div v-if="card.overview.length > 0" class="my_overview">
                <span class="pe-2 fw-bold">Overview:</span>
                <span class="small my_truncate">{{ card.overview }}</span>
            </div>
            <div><span class="pe-2 fw-bold">Nazione:</span> <img :src="movieFlag(card.original_language)" alt=""></div>
            <div><span class="pe-2 fw-bold">Valutazione:</span> <i v-for="(star, index) in rating(card.vote_average)" :key="index"><i v-bind:class="star.class"></i></i></div>
        </div>
    </div>
</template>

<style lang="scss">

</style>