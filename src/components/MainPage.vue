<template>
    <div class="full-parent">
        <header>
            <div class="left-box"></div>
            <div class="middle-box">
                <p>Welcome to SUNY <span style="color: #003E7E">Market</span></p>
            </div>
            <div class="right-box">
                <span>Carts({{ carts }})</span>
            </div>
        </header>
        <div class="product">
            <div class="product-image">
                <img :src="image" />
            </div>
            <div class="product-info">
                <h1>{{ title }}</h1>
                <p v-if="inStock >= 10">In Stock</p>
                <p v-else>Out of Stock</p>
                <ul>
                    <li v-for="detail in details" :key="detail">{{ detail }}</li>
                </ul>
                <div v-for="(variant, index) in variants"
                    :key="variant.variantId"
                    class="color-box"
                    :style="{ backgroundColor: variant.variantColor }"
                    @mouseover="updateProduct(index)">
                </div> 
                <button type="button" class="btn btn-primary"
                    :disabled="inStock == 0"
                    v-on:click="addToCart">
                    Add to Cart
                </button>   
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "MainPage",
    methods: {
        addToCart() {
            this.carts += 1;
        },
        updateProduct(index) {
            this.selectedVariant = index;
        },
    },
    computed: {
        title() {
            return this.brand + " " + this.product;
        },
        image() {
            return this.variants[this.selectedVariant].variantImage;
        },
        inStock() {
            return this.variants[this.selectedVariant].variantQuantity;
        },
    },
    data() {
        return{
            brand: "SUNY",
            product: "Shoes Shop",
            inventory: 0,
            // productImage: require("@/assets/img/shoes-green.jpg"),
            selectedVariant: 0,
            details: ["Canvas", "Size 9", "Gender-neutral"],
            variants: [
                {
                    variantId: "001",
                    variantColor: "green",
                    variantImage: require("@/assets/img/shoes-green.jpg"),
                    variantQuantity: 15,
                },
                {
                    variantId: "002",
                    variantColor: "black",
                    variantImage: require("@/assets/img/shoes-black.jpg"),
                    variantQuantity: 0,
                },
            ],
            carts: 0,
        };
    },
};
</script>

<style>
  @import "../assets/styles/base-layout.css";
  @import "../assets/styles/main-page.css";
</style>