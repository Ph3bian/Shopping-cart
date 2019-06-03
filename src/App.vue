<template>
  <div class="container">
    <div class="row">
      <div class="col-md-7">
        <div class="row">
          <div class="col-md-6" :key="product.id" v-for="product in products">
            <product :isInCart ="isInCart(product)" v-on:add-to-cart="addToCart(product)" :product="product"></product>

          </div>
        </div>
      </div>
      <div class="col-md-5">
        <cart :items="cart" v-on:pay="pay($event)" v-on:remove-from-cart="removeFromCart($event)" ></cart>
      </div>
    </div>

  </div>
</template>

<script>
  import products from '@/products.json';
  import product from '@/components/product';
  import cart from '@/components/cart';

  export default {
    name: 'app',
    data() {
      return {
        products,
        cart: []
      }
    },
    methods: {
      addToCart(product) {
        this.cart.push(product)
      },
      isInCart(product) {
        const item = this.cart.find(item => item.id === product.id);
        if (item) {
          return true
        }
        return false
      }, 
      removeFromCart(product){
        this.cart= this.cart.filter(item => item.id != product.id);
      },
      pay(amount){
        this.cart=[];
        alert(`$ ${amount} Paid. Shopping Completed!`);
      },
    },
    components: {
      product,
      cart
    }
  }
</script>

<style>
  body {
    background-color: #fbf8f3;
  }
</style>