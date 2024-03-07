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
    <div>
        <AppFilm></AppFilm>
        <AppSeries></AppSeries>
    </div>
</template>

<style lang="scss">

</style>
