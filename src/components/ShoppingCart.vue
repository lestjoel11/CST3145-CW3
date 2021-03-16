<template>
    <!-- checkout page -->
    <div class="container-fluid">
        <nav class="navbar navbar-light my-2 font-weight-bold">
            <a class="navbar-brand" style="font-size: 1.5em">
                <span class="fas fa-graduation-cap" style="text-align: center"> After School Club</span>
            </a>
            <div class="navbar-right">
                <button class="btn btn-warning" @click="changeView">
                    Back to Lessons
                </button>
            </div>
        </nav>
        <div class="row d-flex justify-content-center">
            <div class="col-8">
                <div style="background-color: white; border-radius: 20px">
                    <nav class="navbar navbar-light my-2 font-weight-bold">
                        <a class="navbar-brand" style="font-size: 1.5em">
                            <span class="fas fa-shopping-cart" style="text-align: center"> Shopping Cart</span>
                        </a>
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
                            <tbody v-for="lesson in cart" :key="lesson.id">
                                <tr>
                                    <td data-th="Lesson">
                                        <span style="text-align: center; font-size: 1em" v-bind:class="lesson.icon"> {{ lesson.subject }}</span>
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
        </div>
        <div class="row d-flex justify-content-center">
            <div style="background-color: white; border-radius: 20px" class="col-8">
                <form action="/">
                    <nav class="navbar navbar-light my-2 font-weight-bold">
                        <a class="navbar-brand" style="font-size: 1.5em">
                            <span class="fas fa-user" style="text-align: center"> Billing Details</span>
                        </a>
                        <div class="navbar-right">
                            <button @click="checkout" class="btn btn-dark" v-if="!(cust_name === '' || cust_num === '')">
                                Checkout Order
                            </button>
                        </div>
                    </nav>
                    <div class="form-group">
                        <input class="form-control" placeholder="Enter name" style="width: 95%" v-model="cust_name" />
                        <input class="form-control" placeholder="Enter phone" style="width: 95%" v-model="cust_num" />
                    </div>
                </form>
            </div>
        </div>
        <br />
        <h3><strong>Customer Details</strong></h3>
        <h4>Name: {{ this.cust_name }}</h4>
        <br />
        <h4>Number: {{ this.cust_num }}</h4>
    </div>
</template>

<script>
export default {
    props: ["cart"],
    data() {
        return {
            cust_name: "",
            cust_num: "",
        };
    },
    methods: {
        changeView() {
            this.$emit("changeView");
        },
        removeProduct(product) {
            this.$emit("removeProduct", product);
        },
        checkout() {
            alert("Thank You " + this.cust_name);
        },
    },
};
</script>

<style></style>
