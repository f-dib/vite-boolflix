<script>
import {store} from '../store.js';

export default {
    name: 'AppFilm',

    data(){
        return {
            store
        }
    }
}
</script>

<template>
    <ul>
        <li v-for="currentElement in store.popularFilm">{{ currentElement.title }}</li>
    </ul>
</template>

<style lang="scss">

</style>