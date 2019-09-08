<template>
  <div>
    <div class="background">
    </div>
    <div v-if="status === 'processing'" class="popup">
      <h2>Please wait... </h2>
      <div class="waiting">
        We're processing your credit card.<br>
        <img src="../assets/icons/spinner.svg" width="100" height="100" />
      </div>
    </div>
    
    <div v-if="status === 'successful'" class="popup">
      <h2>Thank you for your order! </h2>
      <div class="successful">
        <b>Order number:</b> #8273477376<br>
        <b>Name: </b> Johnny Winter<br>
        <b>Address:</b> 23754, D39, Montreal, Quebec, Canada<br>
        <VButton class="button-continue" v-on:click="continueBuy">
          Continue buying.
        </VButton>
      </div>
    </div>

    <div v-if="status === 'shopping_cart_empty'" class="popup">
      <h2>You got a error! </h2>
      <div class="error">
        Your shoping cart is empty.<br>
        <VButton class="button-continue" v-on:click="continueBuy">
          Continue buying.
        </VButton>
      </div>
    </div>

  </div>
</template>

<script>

import VButton from './VButton';

export default {
    name : "VMessageBox",
    components: {
      VButton
    },
    props: {
      status:  {
        type: String,
        required: true
      }
    },
    methods: {
      continueBuy () {
        this.$emit('changeStatus', 'none');
        location.reload();
      }
    }
}
</script>

<style scoped>
.background {
  position: absolute;
  top:0;
  width: 100vw;
  height: 100vh;
  background-color: #fff;
  opacity: 0.8;
}

.popup {
  
  margin: 70px auto;
  padding: 20px;
  background: #ddd;
  border-radius: 5px;
  width: 50%;
  position: relative;
  opacity: 1;
  -webkit-box-shadow: 10px 10px 18px 0px rgba(0,0,0,0.75);
  -moz-box-shadow: 10px 10px 18px 0px rgba(0,0,0,0.75);
  box-shadow: 10px 10px 18px 0px rgba(0,0,0,0.75);
}

.popup h2 {
  margin-top: 0;
  color: #333;
}

.waiting{
  text-align: center;
}
.successful{
  text-align: left;
}

.error{
  text-align: left;
}

.button-continue {
  margin-top: 20px;
  height: 30px;
  width: 200px;
}
</style>