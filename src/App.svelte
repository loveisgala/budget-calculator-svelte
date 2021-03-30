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

  //Editing Variables
  let setName = "";
  let setAmount = null;
  let setId = null;

  //Reactive
  $: isEditing = setId ? true : false;
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

  /**
   * Reset expenses
   */
  function clearExpenses() {
    expenses = [];
  }

  /**
   * Adds a new expense
   * @param name, amount
   */
  function addExpense({ name, amount }) {
    let expense = { id: Math.random() * Date.now(), name, amount };
    expenses = [expense, ...expenses];
  }

  /**
   * Set modified expense
   * @param id Expense id
   */
  function setModifiedExpense(id) {
    let expense = expenses.find((item) => item.id === id);

    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
  }

  /**
   * Edit the expense
   * @param {name, amount}
   * @returns {Array} Returns new array with new name and amount values
   */
  function editExpense({ name, amount }) {
    expenses = expenses.map((item) => {
      return item.id === setId ? { ...item, name, amount } : { ...item };
    });
    setId = null;
    setAmount = null;
    setName = "";
  }

  //Context
  setContext("remove", removeExpense);
  setContext("clear", clearExpenses);
  setContext("modify", setModifiedExpense);
</script>

<Navbar />
<main class="content">
  <Form
    {addExpense}
    name={setName}
    amount={setAmount}
    {isEditing}
    {editExpense}
  />
  <Totals title="Total Expenses" {total} />
  <ExpensesList {expenses} />
  <Button {expenses} />
</main>
