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
    <div>
        <div class="row mb-5">
            <div class="col-12 text-white ms-2"><h2>FILM</h2></div>
            <AppCard v-for="currentFilm in store.popularFilm" :card="currentFilm"></AppCard>
        </div>
        <div class="row mb-5">
            <div class="col-12 text-white ms-2"><h2>SERIE TV</h2></div>
            <AppCard v-for="currentSerie in store.popularSeries" :card="currentSerie"></AppCard>
        </div>
    </div>
</template>

<style lang="scss">

</style>