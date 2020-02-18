<template>
    <div class="v-catalog-item">
        <img :src=" require('../assets/img/' + product_data.image) "
             class="v-catalog-item__img"
             alt="img">
        <h3 class="v-catalog-item__name">
            {{ product_data.name }}
        </h3>
        <p class="v-catalog-item__price">
            price: <span>{{ product_data.price }} uah</span>
        </p>
        <button
            class="v-catalog-item__btn"
            @click="sendDataToParent">
                add to cart
        </button>
    </div>
</template>

<script>
    export default {
        name: "v-catalog-item",
        props: {
            product_data: {
                type: Object,
                default() {
                    return {}
                }
            }
        },
        methods: {
            sendDataToParent() {
                this.$emit('sendDataToParent', this.product_data.article);
            }
        }
    }
</script>

<style lang="scss">
    .v-catalog-item {
        flex-basis: 20%;
        border-radius: 4px;
        box-shadow: 0 3px 10px -3px #271258;
        padding: 15px;
        margin-bottom: 2%;
        margin-right: 2%;
        &__img {
            max-width: 100%;
        }
        &__btn {
            cursor: pointer;
            display: block;
            background-color: #006f00;
            color: #fff;
            border: 1px solid #006f00;
            outline: none;
            box-shadow: none;
            height: 40px;
            width: 100%;
            &:hover {
                background-color: transparent;
                color: #006f00;
            }
            &:focus {
                border-color: #009f00;
            }
        }
    }
</style>