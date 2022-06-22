<template>
 <!---defines the structure--->
  <div class="nav-bar"></div>
   <div class="cart">Cart({{cart}})</div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img v-bind:src="image">
      </div>
      <div class="product-info">
        <!-- <h1>{{ product }}</h1> -->
        <h2>{{title}}</h2>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <ul>
          <li v-for="detail in details" :key="detail">{{detail}}</li>
        </ul>
        <!-- <div v-for="variant in variants" v-bind:key="variant.id" @mouseover="updateImage(variant.image)" class="color-circle">{{variant.color}}</div> -->
        <!-- <div v-for="variant in variants" v-bind:key="variant.id" @mouseover="updateImage(variant.image)" class="color-circle" :style="{backgroundColor:variant.color}"></div> -->
        <div v-for="(variant,index) in variants" v-bind:key="variant.id" @mouseover="updateVariant(index)" class="color-circle" :style="{backgroundColor:variant.color}"></div>
       <!-- <button class="button" v-on:click="cart +=1 ">Add to cart</button> -->
       <button class="button" v-on:click="addToCart" :disabled="!inStock" :class="{disabledButton: !inStock}">Add to cart</button>
       <!-- <button class="button" @click="removeFromCart" :class="{disabledButton: inventory < 1}">Remove Item</button> -->
        <!-- <p v-if="inventory > 10">In Stock</p>
        <p v-else-if="inventory <=10 && inventory > 0">Likely to be sold out</p>
        <p v-else>Out of Stock</p> -->
      </div>
    </div>
  </div>
 
</template>

<script>
// logic and functionality of the app is maintained here

export default {
  name: "App",
  data() {
    return {
      product: "Socks",
      brand:"Smiles",
      // image: "./assets/images/socks_green.jpg",
      selectedVariant:0,
      // image: "./assets/logo.png"
      // inStock:false,
      //  inventory:1,
      details:['50%cotton', '30%wool','20%polyster'],
      variants:[{
        id:101,color:"green",image:"./assets/socks_blue.jpg",quantity:50
      },
      {
        id:102,color:"blue",image:"./assets/socks_green.jpg",quantity:0
      }
      ],
      cart:0,
    };
  },
  methods:{
    addToCart(){
      this.cart +=1
    },
//     updateImage(variantImage){
// this.image=variantImage
//     },
updateVariant(index){
  this.selectedVariant=index
  console.log(index)
},
    removeFromCart(){
      this.cart -=1 && this.cart !=0
    }
  },
  computed:{
    title(){
      return this.brand + ' ' + this.product
    },
image(){
  return this.variants[this.selectedVariant].image
  
},
inStock(){
  return this.variants[this.selectedVariant].quantity
}
  }
};
</script>

<style>
/* css block where the styles related to the markup in the template is specified */
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
body {
  background-color: #f2f2f2;
  margin: 0px;
  font-family: tahoma;
  color: #282828;
}

.button {
  margin: 30px;
  background-color: #39495c;
  border-radius: 5px;
  font-size: 18px;
  width: 160px;
  height: 60px;
  color: white;
  padding: 20px;
  box-shadow: inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
    inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
    inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
  text-align: center;
  cursor: pointer;
}

.cart {
  margin: 25px 100px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 10px 30px;
  background-color: white;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}

.color-circle {
  width: 50px;
  height: 50px;
  margin-top: 8px;
  border: 2px solid #d8d8d8;
  border-radius: 50%;
}

.disabledButton {
  background-color: #d8d8d8;
  cursor: not-allowed;
}

h1 {
  font-size: 50px;
}

h3 {
  font-size: 25px;
}

img {
  border: 2px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  padding: 15px;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}

input {
  width: 100%;
  height: 40px;
  margin-bottom: 20px;
}

label {
  font-size: 20px;
  margin-bottom: 5px;
}

li {
  font-size: 18px;
}

.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 25px;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.57);
}

.out-of-stock-img {
  opacity: 0.5;
}

p {
  font-size: 22px;
}

.product-display {
  display: flex;
  flex-direction: column;
  padding: 1rem;
}

.product-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.product-image,
.product-info {
  width: 50%;
}

.review-form {
  display: flex;
  flex-direction: column;
  width: 425px;
  padding: 20px;
  margin: 40px;
  border: 2px solid #d8d8d8;
  background-color: white;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}

.review-container {
  width: 425px;
  padding: 20px;
  background-color: white;
  -webkit-box-shadow: 0px 2px 20px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 20px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 20px -12px rgba(0, 0, 0, 0.57);
  margin-left: 40px;
  border: 2px solid #d8d8d8;
}

.review-container li {
  margin-bottom: 30px;
}

.review-form .button {
  display: block;
  margin: 30px auto;
}

select {
  height: 40px;
  font-size: 20px;
  background-color: white;
  cursor: pointer;
}

textarea {
  width: 95%;
  height: 70px;
  padding: 10px;
  font-size: 20px;
  margin-bottom: 20px;
}

ul {
  list-style-type: none;
}

@media only screen and (max-width: 600px) {
  .container {
    flex-direction: column;
  }

  .product-image,
  .product-info {
    margin-left: 10px;
    width: 100%;
  }

  .review-form {
    width: 90%;
  }
}
</style>
