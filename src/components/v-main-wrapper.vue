<template>
    <div class="v-main-wrapper">
        <h1>
            {{ title }}
        </h1>

        <v-catalog />
        <v-cart
            v-if="CART.length"
            :cart_data="CART"
        />
    </div>
</template>

<script>
    import vCatalog from './v-catalog'
    import vCart from './v-cart'
    import {mapGetters} from 'vuex'

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
        computed: {
            ...mapGetters([
                'CART'
            ])
        },
        methods: {},
        watch: {},
        mounted() {
            // console.log('consoleSOLEsole');
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