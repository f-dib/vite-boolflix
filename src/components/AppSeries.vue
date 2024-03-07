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
                return `https://flagcdn.com/16x12/${currentElement}.png`;
        }
    }
}
</script>

<template>
    <h2 class="ms-2 mb-3">SERIE TV</h2>
    <div class="d-flex flex-wrap">
        <div class="my_grid m-auto" v-for="currentElement in store.popularSeries">
            <img  class="img-fluid" :src="seriesImg(currentElement.poster_path)" alt="">
            <div>{{ currentElement.name }}</div>
            <div><img :src="seriesFlag(currentElement.original_language)" alt=""></div>
        </div>
    </div>
</template>

<style lang="scss">

</style>