<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <router-link to="/" class="navbar-brand">Stock Trader</router-link>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item">
          <router-link to="/portfolio" activeClass="active" tag="li">
            <a class="nav-link">Portolio</a>
          </router-link>
        </li>

        <li class="nav-item">
          <router-link to="/stocks" activeClass="active" tag="li">
            <a class="nav-link">Stocks</a>
          </router-link>
        </li>

        <ul class="float-right navbar-nav">
  <li class="nav-item">
          <a class="nav-link" href="#" @click="endDays">End Day</a>
        </li>
        <li class="nav-item dropdown" :class="{open:isDropdownopen}" @click="isDropdownopen = !isDropdownopen"
>
          <a
            class="nav-link dropdown-toggle"
            href="#"
            id="navbarDropdown"
            role="button"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
          >Save & Load</a>
          <div class="dropdown-menu" aria-labelledby="navbarDropdown" >
            <a class="dropdown-item" href="#" @click="saveData">Save Data</a>

            <div class="dropdown-divider"></div>
            <a class="dropdown-item" href="#" @click="loadData">Load Data</a>
          </div>
        </li>
        </ul>
 <strong class="navbar-nav nav-link float-right">Funds:{{funds | currency}}</strong>
      </ul>
    </div>
  </nav>
</template>

<script>
import {mapActions} from 'vuex'
export default {
  data(){
    return{
      isDropdownopen:false
    }
  },
  computed:{
    funds(){
      return this.$store.getters.funds
    }
  },
  methods:{
    ...mapActions({
      randomizeStocks:'randomizeStocks',
      fetchData:'loadData'
    }),
    endDays(){
      this.randomizeStocks();
    },
    saveData(){
      const data={
        funds:this.$store.getters.funds,
        stockPortfolio:this.$store.getters.stockPortfolio,
        stocks:this.$store.getters.stocks
      };
      this.$http.put('data.json',data);
    },
    loadData(){
     this.fetchData();
  }
  }
}
</script>
