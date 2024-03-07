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
    <nav class="navbar bg-black mb-5 position-fixed top-0 start-0 w-100">
        <div class="container-fluid">
            <a class="navbar-brand"><img class="img-fluid-logo" src="/public/img/logo.png" alt=""></a>
            <div class="d-flex">
                <div class="my_avatar me-4"><img class="img-fluid" src="/public/img/Netflix-avatar.png" alt=""></div>
                <div class="d-flex" role="search">
                    <input class="form-control me-1 bg-black" type="search" placeholder="Search" aria-label="Search" v-model="store.searchText" @keyup.enter="$emit('search')">
                    <button @click="$emit('search')" class="btn text-white" type="submit"><i class="fa-solid fa-magnifying-glass"></i></button>
                </div>
            </div>
        </div>
    </nav>
</template>

<style lang="scss">
    .navbar {
        z-index: 12;

        .img-fluid-logo {
        height: 50px!important;
        }

        .my_avatar{
            width: 40px;
            height: 40px;
        }
    }

</style>