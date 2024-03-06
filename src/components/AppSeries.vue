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
        }
    }
}
</script>

<template>
    <div v-for="currentElement in store.popularSeries">
        <img :src="seriesImg(currentElement.poster_path)" alt="">
        <div>{{ currentElement.name }}</div>
    </div>
</template>

<style lang="scss">

</style>