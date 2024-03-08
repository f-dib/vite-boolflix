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
    }
};
</script>

<template>
    <div class="popup d-flex justify-content-center align-items-center fixed-center bg-transparent">
        <div class="card p-4 bg-white position-relative">
            <button type="button" class="btn-close position-absolute my_close" @click="$emit('onClose')"></button>
            <h5 class="card-title">{{ cardData.title ? cardData.title : cardData.name }}</h5>
            <p class="card-text">{{ cardData.overview }}</p>
        </div>
    </div>
</template>

<style>
    .popup {
        width: 60vw;
        height: 50vh;
        
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%); 
        z-index: 20; 
    }

    .my_close{
        top: 10px;
        right: 10px;
    }
</style>