<template>
    <div class="panel">
        <div class="cart-panel">
            <div class="shopping-cart-title">
                <b>SHOPPING CART.</b>
            </div>
            <div v-if="shoppingCartData.shoppingCartItems.length === 0">
                <br>
                Your shopping cart is empty.
            </div>
            <div class="shopping-cart-list">
                <div 
                    v-for="shoppingCartItem in shoppingCartData.shoppingCartItems" 
                    v-bind:key="shoppingCartItem.id"
                >
                    <VShoppingCartPanelItem 
                        v-bind:shoppingCartItem="shoppingCartItem"
                        v-on:incrementItemQuantity="incrementItemQuantity"
                        v-on:decrementItemQuantity="decrementItemQuantity"
                        v-on:removeItem="removeItem"
                    />
                </div>
                <div class="hr-total"></div>
                <VButton 
                    v-if="shoppingCartData.shoppingCartItems.length === 0"
                    v-on:click="continueBuy"
                >
                    Continue Shopping.
                </VButton>
                <div v-else class="total-container">
                    ORDER TOTAL:
                    <div class="total-value">
                        $ {{ shoppingCartData.orderTotal }}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import VShoppingCartPanelItem from './VShoppingCartPanelItem';
import VButton from './VButton';

export default {
    name: 'VShoppingCartPanel',
    components: {
        VShoppingCartPanelItem,
        VButton
    },
    props: {
        shoppingCartData: {
            type: Object,
            required: true
        }
    },
    methods : {
        continueBuy () {
            location.reload();
        },
        incrementItemQuantity(id) {
            this.$emit('incrementItemQuantity',id)
        },
        decrementItemQuantity(id) {
            this.$emit('decrementItemQuantity',id)
        },
        removeItem(id) {
            this.$emit('removeItem',id);
        }
    }
}
</script>

<style scoped>
.panel {
    position: absolute;
    width: 950px;
    height: 480px;
    background-color: #F1F6F9;
    border-radius: 10px;
    left: calc(50vw - (950px / 2));
    top: calc(50vh - (550px / 2));
    -webkit-box-shadow: 0px 0px 25px -13px rgba(0,0,0,0.59);
    -moz-box-shadow: 0px 0px 25px -13px rgba(0,0,0,0.59);
    box-shadow: 0px 0px 25px -13px rgba(0,0,0,0.59);
}

.cart-panel {
    float: left;
    position: relative;
    margin-left: 10%;
    width: 45%;
}

.shopping-cart-title {
    font-size: 11pt;
    width: 75%;
    margin-top: 8%;
}

.shopping-cart-list {
    width: 100%;
    margin-top: 2%;
}

.hr-total{
    margin-top: 3%;
    width: 100%;
    border-top: 1px solid #DDD;
}

.total-container {
    text-align: right;
    font-size: 0.55em;
    color: #aaa;
    margin-top: 6%;
}

.total-value {
    font-size: 1.75rem;
    color: #407CE7;
    font-weight: bold;
    margin-top: -1%;
}

.button {
    margin-top:5%;
    cursor: pointer;
    text-align: center;
    width: 150px;
    height: 30px;
    border-radius: 5px;
    background-color: #407CE7;
    color: #FFF;
}

</style>