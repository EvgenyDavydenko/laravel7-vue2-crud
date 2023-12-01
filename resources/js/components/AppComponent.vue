<template>
    <div>
        <nav-component></nav-component>
        <router-view></router-view>
    </div>
</template>

<script>
    import NavComponent from './NavComponent.vue'
    export default {
        components: { NavComponent },
        mounted() {
            console.log('App mounted.')
        }
    }
</script>
