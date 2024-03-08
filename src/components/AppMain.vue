<script>
import {store} from '../store.js';

import AppCard from './AppCard.vue';

export default {
    name: 'AppMain',
    
    data(){
        return {
            store
        }
    },
    components: {
        AppCard
    }
}
</script>

<template>
    <div class="overflow-x-hidden">
        <div class="text-white ms-2 m-3"><h2>FILM</h2></div>
        <div class="row flex-nowrap ps-2 pe-2 mb-5 ms-1 me-1 overflow-x-auto overflow-y-hidden">
            <AppCard v-for="currentFilm in store.popularFilm" :card="currentFilm"></AppCard>
        </div>

        <div class="text-white ms-2 m-3"><h2>SERIE TV</h2></div>
        <div class="row flex-nowrap ps-2 pe-2 mb-5 ms-1 me-1 overflow-x-auto overflow-y-hidden">     
            <AppCard v-for="currentSerie in store.popularSeries" :card="currentSerie"></AppCard>
        </div>
    </div>
</template>

<style lang="scss">

</style>