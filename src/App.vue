<script>
  export default {
    data: () => {
      return{
        page:"products",
        cart:[]
      }
    },
    components:{
      Products:Products,
      Cart:Cart
    },
    methods:{
      addItemToCart(product){
        let cartIndex = this.cart.findIndex(item => item.name == product.name)
        if(cartIndex !== -1){
          this.cart[cartIndex].quantity = this.cart[cartIndex].quantity + product.quantity
        }
        else{
          this.cart.push(product)
        }
        
      },
      removeItemFromCart(product){
        this.cart.splice(this.cart.indexOf(product),1)
      },
      navigateTo(page){
        this.page = page
      }
      
    }
  }
  import Products from './components/Products.vue'
  import Cart from './components/Cart.vue'
</script>

<template>
 <div>

  <div class="navbar">
    <button class="navbarBtn" v-on:click="navigateTo('products')">Alışverişe devam et</button> 
    <button class="navbarBtn" v-on:click="navigateTo('cart')">Sepete git</button>
  </div>

  <div v-if="this.page == 'products'">
  <Products v-on:addItemToCart="addItemToCart"/>
  </div>
  <div v-if="this.page == 'cart'">
  <Cart v-on:removeItemFromCart="removeItemFromCart" :cart="cart"/>
  </div>
 </div>
</template>

<style scoped>
.navbarBtn{
  margin-left: 200px;
  margin-right: 200px;
}
</style>
