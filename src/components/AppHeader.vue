<script>
export default {
    name: 'AppHeader'
}
</script>

<template>
    <nav class="navbar bg-body-tertiary">
        <div class="container-fluid">
            <a class="navbar-brand">Navbar</a>
            <form class="d-flex" role="search">
            <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
            <button @click="$emit('search')" class="btn btn-outline-success" type="submit">Cerca</button>
            </form>
        </div>
    </nav>
</template>

<style lang="scss">

</style>