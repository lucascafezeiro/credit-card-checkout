<template>
    <div>
        <div class="close_cart">
            Order Total: <span class="total">$ {{this.shoppingCartData.orderTotal}}</span>
            <div class="icon-container" v-on:click="expanded=!expanded">
                <img src="../assets/icons/shopping-list.svg" class="shopping-list-icon" alt="Shopping List">
            </div>
        </div>
        <div class="expandable-container">
            <transition
                name='expand' v-if="expanded">
                <div class="expandable">    
                    <div class="title">SHOPPING CART.</div>
                    <div 
                        class="shopping-cart-item"
                        v-for="shoppingCartItem in shoppingCartData.shoppingCartItems" 
                        v-bind:key="shoppingCartItem.id"
                    >
                        <hr />
                        <VShoppingCartPanelMobileItem
                        v-bind:shoppingCartItem="shoppingCartItem"
                        v-on:incrementItemQuantity="incrementItemQuantity"
                        v-on:decrementItemQuantity="decrementItemQuantity"
                        v-on:removeItem="removeItem"
                        />
                    </div>
                    <div v-if="shoppingCartData.shoppingCartItems.length === 0" style="text-align:center;">
                        <br>
                        <hr>
                        Your shopping cart is empty.
                        <div
                            v-on:click="continueBuy" 
                            class="button continue"
                        >
                            Continue Shopping.
                        </div>
                    </div>
                    <div v-else class="button close" v-on:click="expanded=!expanded">
                        Close.
                    </div>
                </div>
            </transition>
        </div>
    </div>
</template>

<script>

import VShoppingCartPanelMobileItem from './VShoppingCartPanelMobileItem';

export default {
    name: 'VShoppingCartPanelMobile',
    components: {
        VShoppingCartPanelMobileItem
    },
    data () {
        return {
            expanded: false
        }
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
.close_cart {
    padding-top: 0%;
    padding-left: 10%;
    font-size: 0.8em;
    position: absolute;
    float: left;
    top:0px;
    height: 5%;
    background-color: rgb(218, 218, 218);
    width: 90%;
    border-radius: 5px 5px 0px 0px;
    color:#333;
}

.total {
    font-size: 1.3em;
    color:#407CE7;
}
.icon-container {
    cursor: pointer;
    float: right;
    margin-top:2%;
    margin-right: 1%;
}

.shopping-list-icon{
    width: 20px;
    height: 20px;
}

.title{
    padding-top: 5%;
    margin-left: 5%;
}

.shopping-cart-item{
    margin-top: 6%;
}

.expandable-container {
    position: absolute;
    z-index: 100;
    width: 100%;
}

.expandable {
    position: relative;
    background-color:  rgb(218, 218, 218);
    height: 532px;
    width: 100%;
    margin-top: -2px;
    border-radius: 0px 0px 5px 5px;
}

.expand-enter-active,
.expand-leave-active {
    transition: height 0.3s ease-in;
    overflow: hidden;
}

.expand-enter, .expand-leave-to {
    height: 0px;
}

hr {
    border-top: 1pt solid #bbb;
}

.button {
    margin-top:10%;
    cursor: pointer;
    text-align: center;
    height: 30px;
    border-radius: 5px;
    background-color: #407CE7;
    color: #FFF;
}

.close {
    margin-left: 24%;
    width: 150px;
}

.continue {
    margin-left: 8%;
    width: 250px;
}


</style>