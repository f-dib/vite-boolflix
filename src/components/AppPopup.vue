<script>
import {store} from '../store.js';

export default {
    name: 'AppPopup',

    data(){
        return {
            store
        }
    },
    props: {
        cardData: Object,
    },
    methods: {
        posterImg(currentElement){
            return `https://image.tmdb.org/t/p/w1280${currentElement}`;
        }
    }
};
</script>

<template>
    <div class="popup d-flex justify-content-center align-items-center fixed-center bg-transparent">
        <div class="card bg-black text-white position-relative">
            <button type="button" class="btn text-white position-absolute my_close" @click="$emit('onClose')"><i class="fa-solid fa-x"></i></button>
            <div class="w-100 h-50">
                <img class="my_backdrop" :src="posterImg(cardData.backdrop_path)" alt="">
            </div>
            <div class="p-4">
                <h5 class="card-title">{{ cardData.title ? cardData.title : cardData.name }}</h5>
                <p class="small"><span class="fw-bold me-2">Titolo Originale:</span>{{ cardData.original_title ? cardData.original_title : cardData.original_name }}</p>
                <p class="text-truncate" v-if="store.cast.length > 0">
                    <span class="fw-bold me-2">Cast:</span>
                    <span class="me-2" v-for="castMember in store.cast">{{ castMember.name }}, </span>
                </p>
                <p class="card-text" v-if="cardData.overview.length > 0"><span class="fw-bold me-2">Descrizione:</span>{{ cardData.overview }}</p>
            </div>
        </div>
    </div>
</template>

<style>
    .popup {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%); 
        z-index: 20; 

        .card{
            min-width: 55vw;
            min-height: 85vh;
            max-width: 55vw;
            max-height: 85vh;
            box-shadow: 0px 0px 10px gray;
            overflow: auto;

            .my_close{
                top: 10px;
                right: 10px;
            }

            .my_close:hover {
                color: #dc1a28 !important;
            }

            .my_backdrop {
                width: 100%;
                object-fit: cover;
            }

        }
    }


</style>