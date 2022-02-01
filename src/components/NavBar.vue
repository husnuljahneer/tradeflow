<template>
  <nav class="flex items-center justify-between flex-wrap bg-red-500 p-6">
    <div class="flex items-center flex-shrink-0 text-white mr-6"> 
      <router-link to="/"> <span class="text-white"> TradeFlow </span></router-link>
     
    </div>
    <div>
        <div>
            <router-link to="/Cart">Cart</router-link>
            <span class="text-lg font-medium"> {{cart.length}}</span>
        </div>
    </div>
  </nav>
</template>

<script>
import {computed} from 'vue';
import store from '@/store/index';
export default {
    setup(){
        const cart = computed(()=>{
            return store.state.cart;
        });
       
        return {
            cart,
            
        };
    }  ,
    mounted() {
        store.commit('getLocalStorage');
    },
};
</script>

<style>
</style>