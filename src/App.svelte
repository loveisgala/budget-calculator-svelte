<script>
  //Components
  import Navbar from "./components/Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  
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
</script>

<Navbar />
<main class="content">
  <ExpensesList {expenses} {removeExpense} />
</main>
