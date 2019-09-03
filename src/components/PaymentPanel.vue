<template>
  <div class="payment-panel payment-panel-responsive">
        <div class="paymant-form-cointainer">
            <VShoppingCartPanelMobile 
                class="shoppingCartPanelMobile" 
                v-bind:shoppingCartData="purchaseData.shoppingCartData"
                v-on:incrementItemQuantity="incrementItemQuantity"
                v-on:decrementItemQuantity="decrementItemQuantity"
                v-on:removeItem="removeItem"
            />
            <div class="payment-title">
                <b>PAYMENT INFO.</b>
            </div>
            <div class="payment-option">
                <div class="payment-top">
                    <img src="../assets/icons/credit-card-back-symbol.svg" class="credit-card-icon" alt="Credit Card">
                    <span class="credit-card-text">
                        Credit Card
                    </span>
                    <img src="../assets/icons/visa-pay-logo.svg" class="visa-icon" alt="Visa">
                    <img src="../assets/icons/mastercard.svg" class="master-card-icon" alt="Master Card">
                </div>
                <div class="payment-body">
                        Safe money transfer using your banck account. 
                        Visa, Maestro, Discover, American Express.
                </div>
            </div>
            <div class="payment-option paypal">
                <div class="payment-top paypal-top">
                    <img src="../assets/icons/paypal.svg" class="paypal-icon" alt="Paypal">
                    <img src="../assets/icons/paypal-logo.svg" class="paypal-logo-icon" alt="Paypal logo">
                </div>
                <div class="payment-body ">
                        You will be redirected to PayPal website to complete your purchase securely.
                </div>
            </div>
            <FormPayment 
                v-on:submit="submit"
            />
        </div>
    </div>
</template>

<script>

import VShoppingCartPanelMobile from './VShoppingCartPanelMobile';
import FormPayment from './FormPayment';

export default {
    name: 'PaymentPanel',
    components: {
        FormPayment,
        VShoppingCartPanelMobile
    },
    props: {
        purchaseData: {
            type: Object,
            required: true
        }
    },
    methods : {
        submit (formPaymentData) {
            this.$emit('submit', formPaymentData);
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

<style scope>

@media screen and (max-width: 2000px) {
    .payment-panel-responsive {
        top:10%;
        right: 20%;
    }
    .shoppingCartPanelMobile{
        visibility: hidden;
    }
}

@media screen and (max-width: 1200px) {
    .payment-panel-responsive {
        top:10%;
        right: 15%;
    }
    .shoppingCartPanelMobile{
        visibility: hidden;
    }
}

@media screen and (max-width: 1000px) {
    .payment-panel-responsive {
        top:10%;
        right: 8%;
    }
    .shoppingCartPanelMobile{
        visibility: hidden;
    }
}

@media screen and (max-width: 900px) {
    .payment-panel-responsive {
        top:2%;
        left: calc(50vw - (280px / 2));
    }
    .shoppingCartPanelMobile{
        visibility: visible;
    }
}

.payment-panel {
    float: right;
    position: absolute;
    width: 300px;
    height: 560px;
    border-radius: 7px;
    /* gradient background CSS */
    background: rgba(18,23,31,1);
    background: -moz-linear-gradient(45deg, rgba(18,23,31,1) 0%, rgba(26,49,87,1) 100%);
    background: -webkit-gradient(left bottom, right top, color-stop(0%, rgba(18,23,31,1)), color-stop(100%, rgba(26,49,87,1)));
    background: -webkit-linear-gradient(45deg, rgba(18,23,31,1) 0%, rgba(26,49,87,1) 100%);
    background: -o-linear-gradient(45deg, rgba(18,23,31,1) 0%, rgba(26,49,87,1) 100%);
    background: -ms-linear-gradient(45deg, rgba(18,23,31,1) 0%, rgba(26,49,87,1) 100%);
    background: linear-gradient(45deg, rgba(18,23,31,1) 0%, rgba(26,49,87,1) 100%);
    filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#12171f', endColorstr='#1a3157', GradientType=1 )

}

.paymant-form-cointainer {
    width: 100%;
}

.payment-title{
    color: #FFF;
    font-size: 0.8em;
    margin-top:10%;
    margin-left:10%;
}

.payment-option {
    margin-left:10%;
    margin-top: 7%;
    border-radius: 3px;
    border: 1px solid #FFF;
    height: 80px;
    width: 80%;
    padding-top: 2%;
}

.credit-card-text {
    margin-left: 5%;
}

.credit-card-icon {
    width: 18x;
    height: 18px;
}

.visa-icon{
    width: 25x;
    height: 25px;
    margin-left: 32%;
}

.master-card-icon {
    width: 18x;
    height: 18px;
    margin-left: 7%;
}

.paypal-icon{
    width: 15x;
    height: 15px;
    
}

.paypal-logo-icon{
    width: 45x;
    height: 45px;
    margin-left: 2%;
}

.payment-top {
    font-size: 0.5em;
    color: #FFF;
    margin-left: 5%;
    display: flex;
    align-items: center;
}

.paypal-top {
    margin-top: -5%;
    margin-bottom: -6%;
}

.payment-body {
    vertical-align: middle;
    font-size: 0.5em;
    color: #999;
    margin-left: 5%;
    margin-top: 5%;
    padding-right: 1%;
}

.paypal {
    cursor: pointer;
    opacity: 0.3;
    -webkit-user-select: none; /* Chrome all / Safari all */
    -moz-user-select: none;    /* Firefox all             */
    -ms-user-select: none;     /* IE 10+                  */
    user-select: none;        /* Likely future           */
    z-index: -1;
}

.paypal:hover {
    opacity: 1;
}


</style>