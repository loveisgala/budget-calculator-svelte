<script>
  import { afterUpdate, setContext } from "svelte";
  import { onMount } from "svelte";
  //Components
  import Navbar from "./components/Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import Button from "./components/Button.svelte";
  import Totals from "./components/Totals.svelte";
  import Form from "./components/Form.svelte";
  import Modal from "./Modal.svelte";

  //Data
  // import expensesData from "./expenses";

  //Variables
  let expenses = [];

  //Editing Variables
  let setName = "";
  let setAmount = null;
  let setId = null;

  //Toggle form variables
  let isFormOpen = false;

  //Reactive
  $: isEditing = setId ? true : false;
  $: total = expenses.reduce((acc, curr) => {
    return (acc += curr.amount);
  }, 0);

  //Functions

  /**
   * Show Form
   */
  function showForm() {
    isFormOpen = true;
  }

  /**
   * Hide form and reset values
   */
  function hideForm() {
    isFormOpen = false;
    setName = "";
    setAmount = null;
    setId = null;
  }
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
    showForm();
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
  setContext("modify", setModifiedExpense);

  //Local Storage
  /**
   * Set items on Local Storage
   */
  function setLocalStorage() {
    localStorage.setItem("expenses", JSON.stringify(expenses));
  }

  onMount(() => {
    expenses = localStorage.getItem("expenses")
      ? JSON.parse(localStorage.getItem("expenses"))
      : [];
  });
  afterUpdate(() => {
    setLocalStorage();
  });
</script>

<Navbar {showForm} />
<main class="content">
  {#if isFormOpen}
    <Modal>
      <Form
        {addExpense}
        name={setName}
        amount={setAmount}
        {isEditing}
        {editExpense}
        {hideForm}
      />
    </Modal>
  {/if}
  <Totals title="Total Expenses" {total} />
  <ExpensesList {expenses} />
  <Button {clearExpenses} />
</main>
