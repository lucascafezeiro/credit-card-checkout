<template>
    <div class="shopping-cart-list-item">
        <div class="product-picture-container">
            <img v-bind:src="shoppingCartItem.product.pictureUrl" class="product-picture">
        </div>
        <div class="shopping-cart-list-item-descriptions">
            <div class="product-description">
                {{shoppingCartItem.product.description}}
            </div>
            <div class="product-unit-price">
                {{shoppingCartItem.product.price.toFixed(2)}}
            </div>
            <div class="product-detail">
                Size: {{shoppingCartItem.product.size}}
            </div>
            <div class="product-detail">
                Color: {{shoppingCartItem.product.color}}
            </div>
        </div>
        <div class="quantity">
            <VInputNumber  
                v-bind:value="shoppingCartItem.quantity" 
                v-on:increment="$emit('incrementItemQuantity', shoppingCartItem.id)"
                v-on:decrement="$emit('decrementItemQuantity', shoppingCartItem.id)" 
            />
        </div>
        <div class="product-total-price">
            $ {{ shoppingCartItem.totalPrice }}
        </div>
        <div class="x-remove-container">
            <span v-on:click="$emit('removeItem', shoppingCartItem.id)" class="x-remove" > X </span>
        </div>
    </div>
</template>

<script>

import VInputNumber from './VInputNumber'

export default {
    name: 'VShoppingCartPanelItem',
    components: {
        VInputNumber
    },
    props: {
        shoppingCartItem: {
            type: Object,
            required: true
        }
    }
}
</script>

<style scoped>

.shopping-cart-list-item {
    height: 17.5%;
    width: 100%;
    margin-bottom: 1%;
    display: flex;
    align-items: center;
}

.shopping-cart-list-item-descriptions{
    float: left;
    margin-left: 10%;
    width: 47%;
    height: 100%;
}

.product-picture-container{
    float: left;
}

.product-picture{
    width: 60px;
    height: 60px;
    border-radius: 2px;
}

.product-description{
    font-size: 0.8em;
    color: #555;
}

.product-unit-price{
    font-size: 0.6em;
    color: #999;
}

.product-detail{
    font-size: 0.5em;
    color: #999;
}

.quantity {
    font-size: 0.8em;
    width: 15%;
    float: left;
}

.quantity-item {
    float: left;
    color: #555;

}

.product-total-price {
    text-align: right;
    font-size: 0.8em;
    float: left;
    color: #555;
    padding-left: 7%;
    width: 22%;
}

.x-remove-container{
    font-size: 0.8em;
    float: left;
    color: #999;
    width: 15%;
    text-align: right;
}

.x-remove {
    cursor: pointer;
}

</style>