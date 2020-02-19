<template>
    <div class="v-catalog">
        <router-link :to="{name: 'cart', params: {cart_data: CART}}">
            <div class="v-catalog__to-cart">
                Сart: {{ CART.length }}
            </div>
        </router-link>

        <h1>
            {{ title }}
        </h1>
        <ul class="v-catalog__item-list">
            <v-catalog-item
                    v-for="product in PRODUCTS"
                    :key="product.article"
                    :product_data="product"
                    @addToCart="addToCart"
            />
        </ul>
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
        data(){
            return{
                title: 'Catalog. Chose the best only 👀'
            }
        },
        computed: {
            ...mapGetters([
                'PRODUCTS',
                'CART'
            ]),
        },
        methods: {
            ...mapActions([
                'GET_PRODUCTS_FROM_API',
                'ADD_TO_CART',
            ]),
            addToCart(data){
                this.ADD_TO_CART(data);
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
        &__item-list {
            display: grid;
            grid-template-rows: auto;
            grid-template-columns: repeat(4, 1fr);
            grid-gap: 4% 2.5%;
            padding: 30px 0 50px;
        }
        &__to-cart {
            font-size: 18px;
            text-transform: uppercase;
            text-align: center;
            line-height: 40px;
            position: fixed;
            top: 5%;
            right: 5%;
            height: 40px;
            width: auto;
            border-radius: 4px;
            border: 1px solid #aeaeae;
            padding: 0 30px;
            cursor: pointer;
        }
    }
</style>