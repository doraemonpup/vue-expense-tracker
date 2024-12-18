<script setup>
import { ref, computed } from 'vue'
import { useToast } from 'vue-toastification'
import Header from '@/components/Header.vue'
import Balance from '@/components/Balance.vue'
import IncomeExpenses from '@/components/IncomeExpenses.vue'
import TransactionList from '@/components/TransactionList.vue'
import AddTransaction from '@/components/AddTransaction.vue'

const transactions = ref([
  { id: 1, text: 'Flower', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 1598.42 },
  { id: 3, text: 'Book', amount: -10 },
  { id: 4, text: 'Camara', amount: -150 },
])

const toast = useToast()

const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
})

// Get income
const income = computed(() => {
  return transactions.value
    .filter(transaction => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

// Get expenses
const expenses = computed(() => {
  return transactions.value
    .filter(transactions => transactions.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

// Add transaction
const handleTransactionSubmitted = transactionData => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  })

  toast.success('Transaction added')
}

// Generate unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000)
}

// Delete transaction
const handleTransactionDeleted = id => {
  transactions.value = transactions.value.filter(t => {
    return t.id !== id
  })
  toast.success('TransactionList deleted')

  // // if no {} -> return statement not required
  // transactions.value = transactions.value.filter(t => t.id !== id)
}
</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="+total" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <TransactionList
      :transactions="transactions"
      @transactionDeleted="handleTransactionDeleted"
    />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>
