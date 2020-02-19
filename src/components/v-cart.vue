<template>
    <div class="v-cart">
        <router-link :to="{name: 'catalog'}">
            <div class="v-catalog__to-cart">
                Back to catalog
            </div>
        </router-link>
        <h1 v-if="!cart_data.length"> {{ emptyCartTitle }} </h1>
        <h1 v-else> {{ title }} </h1>
        <ul
            v-if="cart_data.length"
            class="v-cart__list">
                <v-cart-item
                        v-for="(item, index) in cart_data"
                        :key="item.article"
                        :cart_item_data="item"
                        @deleteFromCart="deleteFromCart(index)"
                        @decrement="decrement(index)"
                        @increment="increment(index)"
                />
        </ul>
        <div
            v-if="cart_data.length"
            class="v-cart__total">
                <p>
                    Total:
                </p>
                <span>
                    {{ cartTotalCost }} uah
                </span>
        </div>
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
        computed: {
            cartTotalCost() {
                let result = [];

                for (let item of this.cart_data) {
                    result.push(item.price * item.quantity);
                }
                result = result.reduce(function(sum, el){
                    return sum + el;
                });

                return result;
            }
        },
        methods: {
            ...mapActions([
                'DELETE_FROM_CART',
                'INCREMENT_CART_ITEM',
                'DECREMENT_CART_ITEM',
            ]),
            deleteFromCart(index) {
                this.DELETE_FROM_CART(index);
            },
            decrement(index) {
                this.DECREMENT_CART_ITEM(index);
            },
            increment(index) {
                this.INCREMENT_CART_ITEM(index);
            },
        }
    }
</script>

<style lang="scss">
    .v-cart {
        width: 100%;
        display: flex;
        flex-direction: column;

        &__list {
            border-radius: 4px;
            margin: 0;
            display: block;
            background-color: #444;
            padding: 6px 20px;
        }
        &__total {
            font-size: 22px;
            width: 100%;
            display: flex;
            justify-content: flex-start;
            align-items: flex-start;
            padding: 20px;

            p {
                margin: 0;
            }
            span {
                display: block;
                font-weight: bold;
                margin-left: 10px;
            }
        }
    }
</style>