<script>
import { ref, onMounted, computed, watch } from 'vue'
const  expensesItems = ref([]);
const incomesItems = ref([]);

const expence_input_date = ref('')
const expence_input_title = ref('')
const expence_input_choice = ref(null)
const expence_input_prize = ref('')

const income_input_date = ref('')
const income_input_title = ref('')
const income_input_option = ref(null)
const income_input_profit = ref('')

watch(expensesItems, (newExpence) => {
  localStorage.setItem('expensesItems', JSON.stringify(newExpence))
}, {
  deep: true
});
watch(incomesItems, (newIncome) => {
  localStorage.setItem('expensesItems', JSON.stringify(newIncome))
}, {
  deep: true
});

const addExpence = () => {
  if (expence_input_title.value.trim() === '' || expence_input_choice.value === null || expence_input_date.value === null) {
		return
}
expensesItems.value.push({
  dateExpence: expence_input_date.value,
  titleExpence: expence_input_title.value,
  choice: expence_input_choice.value,
  prize: expence_input_prize.value,
  editable: false
	
})
}
const addIncome = () => {
  if (income_input_title.value.trim() === '' || income_input_option.value === null || income_input_date.value === null) {
		return
}
incomesItems.value.push({
  dateIncome: income_input_date.value,
  titleProfit: income_input_title.value,
  option: income_input_option.value,
  profit: income_input_profit.value,
  editable: false
	
})
}

const removeExpence = (expence) => {
	expensesItems.value = expensesItems.value.filter((item) => item !== expence)
}

const removeIncome = (income) => {
	incomesItems.value = incomesItems.value.filter((item) => item !== income)
}
onMounted(() => {
	expensesItems.value = JSON.parse(localStorage.getItem('expensesItems')) || [];
  incomesItems.value = JSON.parse(localStorage.getItem('incomesItems')) || []
})



export default {
  name: "Account",
  data() {
    return {

      expensesCategories: [
        "food&drinks",
        "entertainment",
        "health",
        "obligatories",
      ],
      incomesCategories: ["work", "sell", "donation"],
    };
  },
  methods: {
    addExpence(){
      this.$emit("add-expence");
    },
    addIncome(){
      this.$emit("add-income");
    },

  }
};
</script>

<template>
  <div class="main-container">
    <section id="main-sum">
      <div class="sum-container">
        <h1 id="header" class="all-header">all money this month</h1>

        <div class="sum-box">
          <span class="sum">
            <slot name="sum"></slot>
          </span>
          <span class="dolar">$</span>
        </div>
      </div>
    </section>
    <div id="adding-container">
      <section id="main-expenses">
        <form @submit.prevent="addExpence">
          <div id="add-expense-header">
            <h1 id="header" class="expense-header"><span>add expense</span></h1>
          </div>
          <div class="expenses-inputs">
            <input
              type="text"
              class="income model"
              placeholder="date"
              v-model="expence_input_date"
            />
            <input
              type="text"
              class="expence model"
              placeholder="title"
              v-model="expence_input_title"
            />
            <input
              type="number"
              class="expence model"
              placeholder="prize"
              v-model="expence_input_prize"
            />
            <h4>Pick a category</h4>
            <div class="options">
              <div v-for="choice in expensesCategories">
                <input
                  type="radio"
                  :id="choice"
                 
                  v-model="expence_input_choice"
                  :name="choices"
                  :value="choice"
                />
                <label :for="choice">{{ choice }}</label>
              </div>
            </div>
          </div>
          <input type="submit" value="add expence" class="button" />
        </form>
        <div id="history-expenses-container">
          <h1 id="header" class="expense-header">your expenses this month</h1>
          <h3>expenses sum:</h3>
          <span>
            <slot name="expense-sum"></slot>
          </span>
          <span class="dolar">$</span>

          <div id="history-expenses">
            <div v-for="expence in expensesItems">
              <input type="number" v-model="expence.dateExpence" />
              <input type="text" v-model="expence.titleExpence" />
              <input type="text" v-model="expence.choice" />
              <input type="number" v-model="expence.prize" />
              <div class="actions">
						<button class="delete" @click="removeExpence(expence)">Delete</button>
					</div>

</div>
            
           
          </div>
        </div>
      </section>
      <section id="main-incomes">
        <form @submit.prevent="addIncome">
          <div id="add-income-header">
            <h1 id="header" class="income-header"><span>add income</span></h1>
          </div>
          <div class="incomes-inputs">
            <input
              type="text"
              class="income model"
              placeholder="date"
              v-model="income_input_date"
            />
            <input
              type="text"
              class="income model"
              placeholder="title"
              v-model="income_input_title"
            />
            <input
              type="number"
              class="income model"
              placeholder="profit"
              v-model="income_input_profit"
            />
            
            <h4>Pick a category</h4>
            <div class="options">
              <div v-for="option in incomesCategories">
                <input
                  type="radio"
                  :id="incomeOption"
                  
                  v-model="income_input_option"
                  :name="incomesCategories"
                  :value="incomeOption"
                />
                <label :for="option">{{ option }}</label>
              </div>
            </div>
          </div>
          
          <input type="submit" value="add income" class="button" />
        </form>
        <div id="history-incomes-container">
          <h1 id="header" class="incomes-header">your incomes this month</h1>
          <h3>incomes sum:</h3>
          <span>
            <slot name="incomes-sum"></slot>
          </span>
          <span class="dolar">$</span>
          <div id="history-incomes">
            <div v-for="income in incomesItems">
              


					<div class="income-content">
					
            <input type="number" v-model="income.dateIncome" />
            <input type="text" v-model="income.titleProfit" />
            <input type="text" v-model="income.option" />
            <input type="number" v-model="income.profit" />
					</div>

					<div class="actions">
						<button class="delete" @click="removeIncome(income)">Delete</button>
					</div>
            </div>
         
            
          </div>
        </div>
      </section>
    </div>
  </div>
</template>



<style scoped>
* {
  font-weight: bold;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.main-container {
  width: 100%;
  position: relative;
}
#main-sum {
  height: 20%;
  width: 100%;
  top: 20px;

  align-items: center;
}
.sum-container {
  margin: 0 auto;
  width: 400px;
  align-items: center;
  text-align: center;
}
.sum-box {
  background-color: azure;
  padding: 20px;
}
.dolar {
  font-size: larger;
  padding: 20px;
}
.all-header {
  background-color: rgb(41, 189, 140);
}

#adding-container {
  height: 80%;
  top: 180px;
  width: 100%;
  display: flex;
  position: absolute;
  justify-content: center;
}
#main-expenses,
#main-incomes {
  width: 50%;
  float: center;
}
#main-expenses {
  padding-left: 100px;
  right: 50px;
}

.model {
  padding: 10px;
  margin: 10px;
}
input {
  margin: 5px;
  padding: 5px;
  background-color: rgb(249, 254, 255);
}
.button {
  margin: 5px;
  color: rgb(33, 28, 28);
}
.expense-header span {
  background-color: rgb(204, 128, 166);
}
.income-header span {
  background-color: rgb(124, 185, 116);
  padding: 5px;
  margin: 5px;
}

#header span {
  padding: 5px;
  margin: 5px;
  color: antiquewhite;
}
</style>
