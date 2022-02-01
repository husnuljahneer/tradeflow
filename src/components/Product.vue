<template>
  <div class="w-full max-w-sm mx-auto rounder-md shadow-md overflow-hidden">
    <div
      :style="{ 'background-image': `url(${product.image})` }"
      class="flex items-end justify-end h-56 w-full bg-cover"
    >
      <button class="flex-column items-end justify-end border rounded-full text-white mx-5 "
      :class="isAdded?'bg-red-500 hover:bg:red-400 focus:bg-red:600':'bg-blue-500 hover:bg:blue-400 focus:bg-blue:600'"
      @click="addToCart(product)">
        <span v-if="!isAdded" >add to cart</span>
        <span v-else >remove from cart</span>
      </button>
    </div>
    <div class="px-5 py-3">
      <h3>
        {{ product.name }}
      </h3>
      <span>{{ product.price }} $</span>
    </div>
  </div>
</template>

<script>
import { computed, ref } from "vue";
import store from "@/store/index";

export default {
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  setup(props) {
    const isAdded = ref(false);

    const cart = computed(() => {
      return store.state.cart;
    })

    function addToCart(product) {
      isAdded.value = !isAdded.value;
      if (isAdded.value) {
        store.commit("addToCart", product);
        store.commit("storeProduct")
      } else {
        store.commit("removeProduct", product);
        store.commit("storeProduct")
      }
    }
    function checkAdded(){
        var product = props.product.id;
        var check = cart.value.some((el)=>{
            return el.id === product;
        })
        if (check){
            isAdded.value = true;
        }
        else{
            isAdded.value = false;
        }
    }
    return {
      cart,
      addToCart,
      checkAdded,
      isAdded
    }
  },
  mounted() {
    this.checkAdded();
  },
  
};
</script>

<style>
</style>