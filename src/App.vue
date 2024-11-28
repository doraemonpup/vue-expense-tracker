<script setup></script>

<template>
  <div class="app-container">
    <h1>Expense Tracker</h1>
    <form>
      <input type="text" placeholder="Expense Description" required />
      <input type="number" placeholder="Amount" required />
      <button type="submit">Add Expense</button>
    </form>
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
</style>
