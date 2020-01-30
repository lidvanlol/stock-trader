<template>
  <div class="container">
    <div class="row">
      <div class="col-lg-12">
        <div class="card mt-3">
          <div class="card-header">
            <h3 class="card-title text-center mt-1">
              {{stock.name}}
              <small>Price: {{stock.price}}</small>
            </h3>
          </div>
          <div class="card-body">
            <div class="form-group">
              <div class="float-left" style="width:77%;">
                <input
                  type="number"
                  class="form-control"
                  placeholder="Quantity"
                  v-model="quantity"
                  :class="{danger:insFunds}"
                />
              </div>
              <div class>
                <button
                  class="btn btn-danger ml-2"
                  @click="buyStock"
                  :disabled="quantity <=0 || insFunds"
                >{{insFunds ? 'Insuffitent Funds' : 'Buy'}}</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["stock"],
  data() {
    return {
      quantity: 0
    };
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
    insFunds() {
      return this.quantity * this.stock.price > this.funds;
    }
  },
  methods: {
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      };

      this.$store.dispatch("buyStock", order);
    }
  }
};
</script>
<style scoped>
.danger {
  border: 1px solid red;
}
</style>
