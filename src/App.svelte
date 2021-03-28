<script>
  import { setContext } from "svelte";
  //Components
  import Navbar from "./components/Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import Button from "./components/Button.svelte";
  import Totals from "./components/Totals.svelte";
  import Form from "./components/Form.svelte";

  //Data
  import expensesData from "./expenses";

  //Variables
  let expenses = [...expensesData];

  //Reactive
  $: total = expenses.reduce((acc, curr) => {
    return (acc += curr.amount);
  }, 0);

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
  setContext("remove", removeExpense);
  setContext("remove", clearExpenses);
</script>

<Navbar />
<main class="content">
  <Form />
  <Totals title="Total Expenses" {total} />
  <ExpensesList {expenses} />
  <Button {expenses} />
</main>
