<template>
    <div id="app">
        <h1>{{ siteName }}</h1>
        <div class="container">
            <div v-if="showLessons">
                <productList @addProduct="addToCart" @removeProduct="removeFromCart" @changeView="viewChange" :cart="cart"></productList>
            </div>
        </div>
        <div v-if="!showLessons">
            <shoppingCart @changeView="viewChange" @removeProduct="removeFromCart" :cart="cart"></shoppingCart>
        </div>
    </div>
</template>

<script>
import productList from "./components/ProductList.vue";
import shoppingCart from "./components/ShoppingCart.vue";

export default {
    name: "App",
    data() {
        return {
            siteName: "After School Activities",
            cart: [],
            showLessons: true,
        };
    },
    components: {
        productList,
        shoppingCart,
    },
    methods: {
        addToCart(lesson) {
            if (this.cart.find((item) => item.subject === lesson.subject) !== undefined) {
                this.cart.find((item) => item.subject === lesson.subject).space++;
            } else {
                this.cart.push(JSON.parse(JSON.stringify(lesson)));
                this.cart.find((item) => item.subject === lesson.subject).space = 1;
            }
            lesson.space--;
        },
        removeFromCart(lesson) {
            this.cart.find((item) => item.subject === lesson.subject).space--;
            if (this.cart.find((item) => item.subject === lesson.subject).space == 0) {
                let popItem = this.cart.indexOf(this.cart.find((item) => item.subject === lesson.subject));
                this.cart.splice(popItem, 1);
            }
        },
        viewChange() {
            this.showLessons = !this.showLessons;
        },
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
