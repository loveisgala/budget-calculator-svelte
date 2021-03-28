<script>
  import { setContext } from 'svelte';
  //Components
  import Navbar from "./components/Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import Button from "./components/Button.svelte";
  
  //Data
  import expensesData from "./expenses";
  
  //Variables
  let expenses = [...expensesData];

  //Functions
  /**
   * Remove expense
   * @param id Expense ID
   */
  function removeExpense(id) {
    expenses = expenses.filter((item) => item.id !== id);
  }

  function clearExpenses() {
    expenses = [];
  }

  //Context
  setContext('remove', removeExpense);
  setContext('remove', clearExpenses);
</script>

<Navbar />
<main class="content">
  <ExpensesList {expenses}/>
  <Button {expenses}/>
</main>
