<template>
  <div class="container">
<app-header></app-header>
    <div class="row">
      <div class="col-12">
         <transition name="slide" mode="out-in">
            <router-view></router-view>

         </transition>

      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header'
export default {
components:{
  appHeader:Header
},
created(){
  this.$store.dispatch('setStocks');
}
}
</script>

<style>
  body{
    padding:30px;
  }
  .slide-enter-active{
    animation: slide-in 200ms ease-out forwards;
  }

  .slide-leave-active{
        animation: slide-out 200ms ease-out forwards;

  }
  @keyframes slide-in {
      from{
        transform: translateX(-50px);;
        opacity: 0;
      }
      to{
        transform:translateX(0);
        opacity: 1;
      }
  }
 @keyframes slide-out {
      from{
        transform: translateX(0);;
        opacity: 1;
      }
      to{
        transform:translateX(-50px);
        opacity: 0;
      }

  }
</style>
