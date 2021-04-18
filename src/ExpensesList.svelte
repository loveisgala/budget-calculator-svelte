<script>
  import SectionTitle from "./components/Title.svelte";
  import Expense from "./Expense.svelte";
  import { fly } from 'svelte/transition';
  export let expenses = [];
</script>

<section>
  <SectionTitle title="expense list" />
  <ul>
    {#each expenses as expense, index}
    <div transition:fly={{ x: 200}}>
      <Expense {...expense}  />
    </div>
    {:else}
      <h2>currently you have no expenses</h2>
    {/each}
  </ul>
</section>

<style>
  h2 {
    text-transform: capitalize;
  }
</style>
