<template>
    <div class="v-catalog">
        <v-catalog-item
            v-for="product in PRODUCTS"
            :key="product.article"
            :product_data="product"
            @sendDataToParent="showItemArticle"
        />
    </div>
</template>

<script>
    import vCatalogItem from './v-catalog-item'
    import {mapActions, mapGetters} from 'vuex'

    export default {
        name: "v-catalog",
        components: {
            vCatalogItem
        },
        props: {},
        data() {
            return {

            }
        },
        computed: {
            ...mapGetters([
                'PRODUCTS'
            ]),
        },
        methods: {
            ...mapActions([
                'GET_PRODUCTS_FROM_API'
            ]),
            showItemArticle(data){
                console.log(data);
            }
        },
        mounted() {
            this.GET_PRODUCTS_FROM_API()
            .then((response) => {
                if (response.data) {
                    console.log('Data arrived!')
                }
            });
        }
    }
</script>

<style lang="scss">
    .v-catalog {
        display: flex;
        flex-wrap: wrap;
        justify-content: flex-start;
    }
</style>