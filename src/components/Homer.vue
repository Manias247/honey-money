<template>
  <Account
  @add-expence="addExpence"
  @add-income="addIncome"
  :statusEx="addExpenceStatus"
  :statusIn="addIncomeStatus">
   
  </Account>

</template>

<script>
import Account from './Account.vue';
export default {
  name: "Homer",
  components: {
    Account
  },
  
  data(){
    return {
      addExpenceStatus: false,
      addIncomeStatus: false, 
    }
  },
  methods: {
    addExpence(){
      
        this.addExpenceStatus = true;
      
    },
    addIncomeStatus(){
      
        this.addIncomeStatus = true;
      }
    }
  
};
</script>

<style scoped>


</style>
