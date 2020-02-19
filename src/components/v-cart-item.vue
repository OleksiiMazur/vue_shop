<template>
    <div class="v-cart-item">
        <img :src=" require('../assets/img/' + cart_item_data.image) "
             class="v-cart-item__img"
             alt="img">
        <div class="v-cart-item__info">
            <h3>
                {{ cart_item_data.name }}
            </h3>
            <p class="v-cart-item__price">
                <span>{{ cart_item_data.price }} uah</span>
            </p>
            <p class="v-cart-item__article">
                {{ cart_item_data.article }}
            </p>
        </div>
        <div class="v-cart-item__quantity">
            <span>Qty:</span>
            <button
                class="v-cart-item__quantity-btn"
                @click="decrementItem"> - </button>
            {{ cart_item_data.quantity }}
            <button
                class="v-cart-item__quantity-btn"
                @click="incremenItem"> + </button>
        </div>
        <button
                @click="deleteFromCart"
                class="v-cart-item__close-btn"
        >x</button>
    </div>
</template>

<script>
    export default {
        name: "v-cart-item",
        props: {
            cart_item_data: {
                type: Object,
                default() {
                    return {}
                }
            }
        },
        mounted() {
            this.$set(this.cart_item_data, 'quantity', 1);
        },
        methods: {
            deleteFromCart() {
                this.$emit('deleteFromCart');
            },
            decrementItem() {
                this.$emit('decrement');
            },
            incremenItem() {
                this.$emit('increment');
            }
        },
    }
</script>

<style lang="scss">
    .v-cart-item {
        z-index: 1;
        width: 100%;
        display: flex;
        background-color: #fff;
        justify-content: space-between;
        align-items: center;
        flex-wrap: nowrap;
        max-height: 150px;
        padding: 14px;
        margin: 14px 0;
        box-shadow: 0 3px 12px -5px #070707;
        border-radius: 4px;

        &__img {
            max-width: 150px;
        }
        &__close-btn {
            font-weight: bold;
            display: block;
            height: 36px;
            font-size: 20px;
            width: 36px;
            background-color: #d13a00;
            color: #fff;
            box-shadow: none;
            outline: none;
            border: none;
            border-radius: 3px;
        }
        &__quantity {
            span {
                display: block;
                margin-bottom: 20px;
            }
            &-btn {
                display: inline-block;
                height: 30px;
                width: 30px;
                font-size: 22px;
                font-weight: bold;
                background-color: darkgreen;
                color: #fff;
                border-radius: 4px;
                border: none;
                outline: none;
            }
        }
    }
</style>