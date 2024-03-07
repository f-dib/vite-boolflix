<script>
import {store} from '../store.js';

export default {
    name: 'AppSeries',
    
    data(){
        return {
            store
        }
    },
    methods: {
        seriesImg(currentElement){
            return `https://image.tmdb.org/t/p/w342${currentElement}`;
        },
        seriesFlag(currentElement){
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
    <h2 class="ms-2 mb-3">SERIE TV</h2>
    <div class="d-flex flex-wrap mb-5">
        <div class="my_grid m-auto position-relative" v-for="currentElement in store.popularSeries">
            <img  class="my_img-fluid" :src="seriesImg(currentElement.poster_path)" alt="">

            <div class="position-absolute my_overlay text-white p-2 d-flex flex-column justify-content-center">
                <div>{{ currentElement.name }}</div>
                <div v-if="currentElement.overview.length > 0" class="my_overview">
                    <span class="pe-2 fw-bold">Overview:</span>
                    <span class="small my_truncate">{{ currentElement.overview }}</span>
                </div>
                <div><img :src="seriesFlag(currentElement.original_language)" alt=""></div>
                <div><i v-for="(star, index) in rating(currentElement.vote_average)" :key="index"><i v-bind:class="star.class"></i></i></div>
            </div>
        </div>
    </div>
</template>

<style lang="scss">

</style>