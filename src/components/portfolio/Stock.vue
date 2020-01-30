<template>
  <div class="col-lg-12">
    <div class="card mt-3">
      <div class="card-header">
        <h3 class="card-title text-center mt-1">
          {{stock.name}}
          <small>Price: {{stock.price}} || Quantity: {{stock.quantity}}</small>
        </h3>
      </div>
      <div class="card-body">
        <div class="float-left">
          <input type="number" class="form-control" placeholder="Quantity" v-model="quantity" :class="{danger:insQunt}" style="width:75%"/>
        </div>
        <div class>
          <button class="btn btn-danger ml-1" @click="sellStock" :disabled="quantity <=0 || insQunt">{{insQunt ? 'Not Enaugh Stocks' : 'Sell'}}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {mapActions} from 'vuex';
export default {
  props: ["stock"],
  data() {
    return {
      quantity: 0
    };
  },
  methods: {
    ...mapActions({
      placeSellOrder:'sellStock'
    }),
      sellStock(){
        const order = {
          stockId:this.stock.id,
          stockPrice:this.stock.price,
          quantity:this.quantity
        };
        this.placeSellOrder(order);
        this.quantity = 0;
      }
  },
  computed:{
    insQunt(){
      return this.quantity>this.stock.quantity;
    }
  }
}
</script>

<style scoped>
  .danger{
    border:1px solid red
  }
</style>
