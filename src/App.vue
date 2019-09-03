<template>
  <div id="app">
    <CreditCardChekout />
  </div>
</template>

<script>

import CreditCardChekout from './components/CreditCardChekout';

export default {
  name: 'app',
  components: {
    CreditCardChekout
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Kanit&display=swap');

  #app {
    background-image: url("./assets/imgs/background.gif");
    background-position:center center;
    background-repeat:no-repeat;
    position: fixed;
    font-size: 14pt;
    font-family: 'Kanit', sans-serif;
    overflow-y: auto;
    width: 100%;
    height: 100%;
  }
  
</style>
