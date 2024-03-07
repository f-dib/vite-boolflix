<script>
import {store} from '../store.js';

export default {
    name: 'AppHeader',

    data(){
        return {
            store
        }
    }
}
</script>

<template>
    <nav class="navbar bg-body-tertiary mb-5">
        <div class="container-fluid">
            <a class="navbar-brand">Navbar</a>
            <div class="d-flex" role="search">
            <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" v-model="store.searchText">
            <button @click="$emit('search')" class="btn btn-outline-success" type="submit">Cerca</button>
            </div>
        </div>
    </nav>
</template>

<style lang="scss">

</style>