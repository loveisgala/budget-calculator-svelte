<style>
  h2 {
    text-transform: capitalize;
  }
</style>

<script>
  import SectionTitle from "./components/Title.svelte";
  import Expense from "./Expense.svelte";
  export let expenses = [];
  export let removeExpense;
</script>

<section>
  <SectionTitle title="expense list" />
  <ul>
    {#each expenses as expense, index}
      <Expense {...expense} {removeExpense}/>
    {:else}
      <h2>currently you have no expenses</h2>
    {/each}
  </ul>
</section>

