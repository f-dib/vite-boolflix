<script>
import AppFilm from './AppFilm.vue';
import AppSeries from './AppSeries.vue';

export default {
    name: 'AppMain',

    components: {
        AppFilm,
        AppSeries
    }
}
</script>

<template>
    <div class="color">
        <h1 class="text-center">ciao</h1>
        <AppFilm></AppFilm>
        <AppSeries></AppSeries>
    </div>
</template>

<style lang="scss">

</style>
