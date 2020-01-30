<template>
  <div>
    <h1 class="mt-2">Trade or view your Portfolio</h1>
    <h6 class="mt-1">You may save & load your data</h6>
    <h6 class="mt-1">Click on 'End Day' to begin a new Day</h6>
    <hr>
    <p >Your Funds: {{funds | currency}}</p>
  </div>
</template>

<script>
export default {
    computed:{
      funds(){
        return this.$store.getters.funds;
      }
    }
}
</script>
