<template>
    <div>
        <div class="shopping-cart-container">
            <VShoppingCartPanel 
                v-bind:shoppingCartData="purchaseData.shoppingCartData"
                v-on:incrementItemQuantity="incrementItemQuantity"
                v-on:decrementItemQuantity="decrementItemQuantity"
                v-on:removeItem="removeShoppingCartItem"
            />
        </div>
        <div class="payment-panel-container">
            <VPaymentPanel 
                v-bind:purchaseData="purchaseData"
                v-on:incrementItemQuantity="incrementItemQuantity"
                v-on:decrementItemQuantity="decrementItemQuantity"
                v-on:removeItem="removeShoppingCartItem"
                v-on:submit="submitOrder"
            />
        </div>
        <VMessageBox 
            v-if="status !== 'none'" 
            v-on:changeStatus="changeStatus"
        />
    </div>
</template>

<script>

import VShoppingCartPanel from './VShoppingCartPanel';
import VPaymentPanel from './VPaymentPanel';
import VMessageBox from './VMessageBox';

export default {
  name: 'app',
  components: {
    VShoppingCartPanel,
    VPaymentPanel,
    VMessageBox
  },
  data () {
    return {
        status : 'none',
        purchaseData : {
            shoppingCartData: {
            shoppingCartItems: [
                {
                    id: 1,
                    product: {
                        pictureUrl: require('../assets/imgs/product1.gif'),
                        description: 'T-short Girl Power',
                        price: 28.55,
                        size: 'S',
                        color: 'Burgundy',
                        totalStock: 10
                    },
                    quantity: 2,
                    totalPrice: 57.10
                },
                {
                    id: 2,
                    product: {
                        pictureUrl: require('../assets/imgs/product2.gif'),
                        description: '2019 Fashion',
                        price: 30.50,
                        size: 'S',
                        color: 'Black, blue, white',
                        totalStock: 10
                    },
                    quantity: 2,
                    totalPrice: 61.00
                },
                {
                    id: 3,
                    product: {
                        pictureUrl: require('../assets/imgs/product3.gif'),
                        description: 'New Women',
                        price: 40.00,
                        size: 'S',
                        color: 'pink',
                        totalStock: 10
                    },
                    quantity: 2,
                    totalPrice: 80.00
                }
            ],
            orderTotal: 0
            },
            paymentData: {}
        }
    }
  },
  methods: {
    submitOrder (paymentData) {
        this.purchaseData.paymentData = paymentData;
        this.status = 'waiting'
    },
    changeStatus  (status) {
        this.status = status
    },
    incrementItemQuantity (id) {
      let index = this.purchaseData.shoppingCartData.shoppingCartItems.findIndex(
        (item) => (item.id === id)
      )
      if (this.purchaseData.shoppingCartData.shoppingCartItems[index].quantity < 
          this.purchaseData.shoppingCartData.shoppingCartItems[index].product.totalStock
      ) {
        this.purchaseData.shoppingCartData.shoppingCartItems[index].quantity++;
        this.updateTotalPriceItem(index);
        this.updateOrderTotal();
      }
    },
    decrementItemQuantity (id) {
      let index = this.purchaseData.shoppingCartData.shoppingCartItems.findIndex(
        (item) => (item.id === id)
      )
      if (this.purchaseData.shoppingCartData.shoppingCartItems[index].quantity > 1) {
        this.purchaseData.shoppingCartData.shoppingCartItems[index].quantity--;
        this.updateTotalPriceItem(index);
        this.updateOrderTotal();
      }
    },
    removeShoppingCartItem (id) {
      this.purchaseData.shoppingCartData.shoppingCartItems = 
        this.purchaseData.shoppingCartData.shoppingCartItems.filter( (item) => (item.id) !== id );
      this.updateOrderTotal();
    },
    updateOrderTotal () {
      this.purchaseData.shoppingCartData.orderTotal = 
        this.purchaseData.shoppingCartData.shoppingCartItems.reduce(
          (sum, item) => {
              return ( sum + Number( item.product.price * item.quantity) );
          },0
        ).toFixed(2);
    },
    updateTotalPriceItem (index) {
      this.purchaseData.shoppingCartData.shoppingCartItems[index].totalPrice = 
        this.purchaseData.shoppingCartData.shoppingCartItems[index].quantity *
        this.purchaseData.shoppingCartData.shoppingCartItems[index].product.price;
    }
  },
  mounted () {
    this.updateOrderTotal();
  }
}
</script>

<style>

.payment-panel-container {
   z-index: 5;
}

@media screen and (max-width: 900px) {
  .shopping-cart-container {
    visibility: hidden;
    display: none;
  }
}
  
</style>
