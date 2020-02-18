<template>
    <div class="v-main-wrapper">
        <h1>
            {{ title }}
        </h1>

        <v-cart />
        <v-catalog />
    </div>
</template>

<script>
    import vCatalog from './v-catalog'
    import vCart from './v-cart'

    export default {
        name: 'v-main-wrapper',
        components: {
            vCatalog,
            vCart,
        },
        props: {},
        data(){
            return{
                title: 'Main wrapper'
            }
        },
        computed: {},
        methods: {},
        watch: {},
        mounted() {
            console.log('consoleSOLEsole');
        }
    }
</script>

<style lang="scss">
    .v-main-wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        max-width: 90%;
        margin: 0 auto;
    }
</style>