<template>
    <div class="v-cart">
        <router-link :to="{name: 'catalog'}">
            <div class="v-catalog__to-cart">
                Back to catalog
            </div>
        </router-link>
        <h1 v-if="!cart_data.length"> {{ emptyCartTitle }} </h1>
        <h1 v-else> {{ title }} </h1>
        <p
            class="v-cart__empty">

        </p>
        <v-cart-item
            v-for="(item, index) in cart_data"
            :key="item.article"
            :cart_item_data="item"
            @deleteFromCart="deleteFromCart(index)"
        />
    </div>
</template>

<script>
    import vCartItem from './v-cart-item'
    import {mapActions} from 'vuex'

    export default {
        name: "v-cart",
        components: {
            vCartItem
        },
        props: {
            cart_data: {
                type: Array,
                default() {
                    return []
                }
            }
        },
        data() {
            return {
                title: 'Cart. Let`s buy svth!)🥋',
                emptyCartTitle: '🙄 At first add smth to cart',
            }
        },
        computed: {},
        methods: {
            ...mapActions([
                'DELETE_FROM_CART'
            ]),
            deleteFromCart(index) {
                this.DELETE_FROM_CART(index);
            }
        }
    }
</script>

<style lang="scss">
    .v-cart {
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }
</style>