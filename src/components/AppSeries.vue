<script>
import {store} from '../store.js';

export default {
    name: 'AppSeries',
    
    data(){
        return {
            store
        }
    }
}
</script>

<template>
    <ul>
        <li v-for="currentElement in store.popularSeries">{{ currentElement.name }}</li>
    </ul>
</template>

<style lang="scss">

</style>