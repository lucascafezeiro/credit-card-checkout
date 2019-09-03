<template>
    <div>
        <div class="container">
            <div class="picture-container">
                <img v-bind:src="shoppingCartItem.product.pictureUrl" class="product-picture">
            </div>
            <div class="product-detail-container">
                <div class="description">
                    {{shoppingCartItem.product.description}}
                </div>
                <div class="details-product"> 
                    <div class="field-product">
                        Unit Price: {{shoppingCartItem.product.price.toFixed(2)}}
                    </div>
                    <div class="field-product">
                        Size: {{shoppingCartItem.product.size}}
                    </div>
                    <div class="field-product">
                        Color: {{shoppingCartItem.product.color}}
                    </div>
                </div>
            </div>
            <div class="x-remove">
                 <span v-on:click="$emit('removeItem', shoppingCartItem.id)" > X </span>
            </div>
        </div>
        <div>
            <div class="quantity-price-container">
                <div class="quantity">
                    <VInputNumber  
                        v-bind:value="shoppingCartItem.quantity" 
                        v-on:increment="$emit('incrementItemQuantity', shoppingCartItem.id)"
                        v-on:decrement="$emit('decrementItemQuantity', shoppingCartItem.id)" 
                    />
                </div>
                <div class="product-total-price">
                    $ {{ shoppingCartItem.totalPrice.toFixed(2) }}
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import VInputNumber from './VInputNumber';

export default {
    name: 'VShoppingCartPanelMobileItem',
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

.container{
    margin-left: 5%;
    display: flex;
    align-items: flex-start;
        
}

.product-detail-container{
    height: 100%;
}

.description {
    font-size: 0.8em;
    margin-left: 5%;
}

.details-product {
    font-size: 0.5em;
    color: #999;
    display: flex;
    flex-wrap: wrap;
}

.field-product {
    margin-left: 5pt;
}

.product-picture{
    height: 60px;
    width: 60px;
    border-radius: 2px;
}

.quantity-price-container {
    display: flex;
    align-items: flex-end;
}

.quantity {
    margin-left: 5pt;
    width: 30%;
}

.product-total-price {
    margin-right: 5%;
    color: #555;
    text-align: right;
    width: 70%;
}

.x-remove {
    cursor: pointer;
    text-align: right;
    margin-right: 5%;
    width: 20%;
    height: 100%;
    color: #555;
}
</style>