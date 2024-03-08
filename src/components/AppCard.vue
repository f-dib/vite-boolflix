<script>
import axios from 'axios';

import {store} from '../store.js';
import AppPopup from './AppPopup.vue';

export default {
    name: 'AppCard',

    components: {
        AppPopup
    },
    props: {
        card: Object,
    },

    data(){
        return {
            store,
            showPopup: false
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
        },
        openPopup() {
            this.showPopup = true;
            document.body.style.overflow = 'hidden';

            axios.get(`https://api.themoviedb.org/3/movie/${this.card.id}/credits?language=it-IT?&api_key=e99307154c6dfb0b4750f6603256716d`).then(res3 => {

                this.store.cast = res3.data.cast.slice(0, 6)
                console.log(this.store.cast)

            }).catch(err => {
            console.log(err)
            })
        },
        closePopup() {
            this.showPopup = false;
            document.body.style.overflow = 'auto';
            this.store.cast = ''
        }
    }
}
</script>

<template>
    <div class="my_grid p-0 position-relative col-2 m-1" @click="openPopup">
        <img class="my_img-fluid" :src="movieImg(card.poster_path)" alt="">
        
        <div class="position-absolute my_overlay text-white p-2 d-flex flex-column justify-content-center">
            <div><span class="pe-2 fw-bold">Titolo:</span> {{ card.title ? card.title : card.name }} </div>
            <div v-if="card.overview.length > 0" class="my_overview text-truncate">
                <span class="pe-2 fw-bold">Descrizione:</span>
                <span class="small">{{ card.overview }}</span>
            </div>
            <div><span class="pe-2 fw-bold">Nazione:</span> <img :src="movieFlag(card.original_language)" alt=""></div>
            <div><span class="pe-2 fw-bold">Valutazione:</span> <i v-for="(star, index) in rating(card.vote_average)" :key="index"><i v-bind:class="star.class"></i></i></div>
            <div><h6 class="text-uppercase text-center mt-5">scopri di più</h6></div>
        </div>
    </div>
    <AppPopup v-if="showPopup" :cardData="card" @onClose="closePopup()" />
</template>

<style lang="scss">

</style>