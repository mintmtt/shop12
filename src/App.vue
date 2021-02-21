<template>
  <div id="app">
      
    <Cart />
   
  </div>
</template>

<script>
import Cart from './components/Cart'

export default {
  name: 'app',
  components: {
    Cart
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #254704;
  background-color: rgb(255, 231, 249);
}
</style>
