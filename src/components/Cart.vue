<script>
export default{
    name:"Cart",
    data:()=>{
        return{

        }
    },
    props:["cart"],
    methods:{
        removeItemFromCart(product){
            
            this.$emit("removeItemFromCart",product)
        },
        decrase(product){
            if(product.quantity-1==0){
                this.removeItemFromCart(product)
            }
            else{
                product.quantity = product.quantity-1
            }
        },       
        increase(product){
            product.quantity = product.quantity+1
        }        
    }
}
</script>
<template>
<div>
    <h1>Sepetiniz</h1>
    <div class="cart">
        <div v-for="(product,index) in cart" :key="index">
        <img :src=product.image alt="product.name">
        <h3>{{ product.name }}</h3>
        <h4>{{ product.price }}$</h4>
        <div class="countSection">
            <button class = "decrement" v-on:click="decrase(product)">azalt</button>
            <h4>{{ product.quantity }} Adet</h4>
            <button class="increment" v-on:click="increase(product)">arttır</button>
        </div>
        <button v-on:click="removeItemFromCart(product)">Sepetten Kaldır</button>
        </div>
    </div>
</div>
</template>
<style scoped>
.cart{
    display: grid;
    grid-template-columns: 300px 300px 300px 300px;
    grid-template-rows: auto;
    row-gap: 50px;
}
.countSection{
    display: flex;
    justify-content: center;
}
.decrement,.increment {
    height: 50px;
    margin: 10px;
}
</style>