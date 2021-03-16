<template>
    <main>
        <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5">
            <div v-for="lesson in products" :key="lesson.id">
                <div class="col mb-4">
                    <div class="card" style="border-radius: 25px">
                        <div class="card-body">
                            <h5 class="card-title">{{ lesson.subject }}</h5>
                            <div class="d-flex justify-content-center" style="padding-bottom: 1rem">
                                <span
                                    style="
                    font-size: 10vw;
                    text-shadow: 3px 6px rgba(255, 165, 0, 0.75);
                  "
                                    v-bind:class="lesson.icon"
                                ></span>
                            </div>
                            <div class="card-text">
                                Price: {{ lesson.price }}$ <br />
                                Location: {{ lesson.location }}<br />
                                Space: {{ lesson.space }}<br />
                            </div>
                            <br />
                            <button @click="addProduct(lesson)" class="btn btn-warning" v-if="canAddToCart(lesson)">
                                Add item
                            </button>
                            <button class="btn btn-secondary" disabled v-else>
                                Sold Out!
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- display cart only  > 0 -->
        <div v-if="this.cart.length > 0">
            <div style="background-color: white; border-radius: 20px">
                <nav class="navbar navbar-light my-2 font-weight-bold">
                    <a class="navbar-brand" style="font-size: 1.5em">
                        <span class="fas fa-shopping-cart" style="text-align: center"> Shopping Cart</span>
                    </a>
                    <div class="navbar-right">
                        <button class="btn btn-warning" @click="changeView">
                            Checkout
                        </button>
                    </div>
                </nav>
                <div>
                    <table class="table table-condensed" id="cart">
                        <thead>
                            <tr>
                                <th style="width: 40%">Lesson</th>
                                <th style="width: 25%">Price</th>
                                <th style="width: 25%">Quantity</th>
                                <th style="width: 40%">Remove</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="lesson in cart" :key="lesson.id">
                                <td data-th="Lesson">
                                    <span style="text-align: center; font-size: 1.5em" v-bind:class="lesson.icon"> {{ lesson.subject }}</span>
                                </td>
                                <td data-th="Price">{{ lesson.price }}</td>
                                <td data-th="Quantity">{{ lesson.space }}</td>
                                <td data-th="Remove">
                                    <button @click="removeProduct(lesson)" class="btn btn-danger">
                                        Remove
                                    </button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
export default {
    name: "ProductsList",
    props: ["cart"],
    data() {
        return {
            products: [
                {
                    id: 1,
                    subject: "Maths",
                    location: "London",
                    price: 399,
                    space: 5,
                    icon: "fas fa-square-root-alt",
                },
                {
                    id: 2,
                    subject: "Science",
                    location: "Dubai",
                    price: 699,
                    space: 5,
                    icon: "fas fa-atom",
                },
                {
                    id: 3,
                    subject: "Geography",
                    location: "Malta",
                    price: 249,
                    space: 5,
                    icon: "fas fa-globe-americas",
                },
                {
                    id: 4,
                    subject: "Arts",
                    location: "Malta",
                    price: 599,
                    space: 5,
                    icon: "fas fa-palette",
                },
                {
                    id: 5,
                    subject: "Business",
                    location: "London",
                    price: 999,
                    space: 5,
                    icon: "fas fa-briefcase",
                },
                {
                    id: 6,
                    subject: "Law",
                    location: "Malta",
                    price: 749,
                    space: 5,
                    icon: "fas fa-landmark",
                },
                {
                    id: 7,
                    subject: "Engineering",
                    location: "Dubai",
                    price: 1249,
                    space: 5,
                    icon: "fas fa-laptop-code",
                },
                {
                    id: 8,
                    subject: "Accounting",
                    location: "Dubai",
                    price: 1100,
                    space: 5,
                    icon: "fas fa-balance-scale-right",
                },
                {
                    id: 9,
                    subject: "Architecture",
                    location: "London",
                    price: 899,
                    space: 5,
                    icon: "fas fa-torii-gate",
                },
                {
                    id: 10,
                    subject: "Medicine",
                    location: "Malta",
                    price: 649,
                    space: 5,
                    icon: "fas fa-stethoscope",
                },
            ],
        };
    },
    methods: {
        addProduct(product) {
            this.$emit("addProduct", product);
        },
        removeProduct(product) {
            this.products.find((item) => item.subject === product.subject).space++;
            this.$emit("removeProduct", product);
        },
        changeView() {
            this.$emit("changeView");
        },
        canAddToCart(lesson) {
            return 5 > 5 - lesson.space;
        },
    },
};
</script>

<style></style>
