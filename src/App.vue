<script setup>
import { ref, computed } from 'vue'

// Reactive data
const expenses = ref([])
const newExpense = ref({
  description: '',
  amount: null,
})

// Methods
const addNewExpense = () => {
  if (newExpense.value.description.length > 0 && newExpense.value.amount >= 0) {
    expenses.value.push({ ...newExpense.value })
    newExpense.value.description = ''
    newExpense.value.amount = null
  }
}

const deleteExpense = index => {
  expenses.value.splice(index, 1)
}

// Computed property for total
const total = computed(() => {
  return expenses.value.reduce((sum, expense) => sum + expense.amount, 0)
})
</script>

<template>
  <div class="app-container">
    <h1>💸 Expense Tracker</h1>
    <form @submit.prevent="addNewExpense">
      <input
        v-model="newExpense.description"
        type="text"
        placeholder="Expense Description"
        required
      />
      <input
        v-model="newExpense.amount"
        type="number"
        placeholder="Amount"
        min="0"
        step="0.01"
        required
      />
      <button type="submit">Add Expense</button>
    </form>

    <h2>Expenses</h2>
    <ul>
      <li v-for="(expense, index) in expenses" :key="index">
        <span>{{ expense.description }} - {{ expense.amount }}€</span>
        <button @click="deleteExpense(index)">Delete</button>
      </li>
    </ul>

    <h2>Total: {{ total }}€</h2>
  </div>
</template>

<style scoped>
.app-container {
  padding: 20px;
  max-width: 600px;
  margin: 0 auto;
}
form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
input {
  padding: 5px;
}
input:first-child {
  width: 200px;
}
input:nth-child(2) {
  width: 100px;
}
button {
  padding: 5px 10px;
  background-color: #007bff;
  color: #fcfdfd;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  color: #e5efef;
  background-color: #0056b3;
}
ul {
  /* list-style: none; */
  padding: 0;
}
li {
  display: flex;
  justify-content: space-between;
  padding: 5px 0;
}
</style>
