<script>
  import { getContext } from "svelte";

  export let clearExpenses;
</script>

<button
  type="button"
  class="btn btn-primary btn-block"
  on:click={clearExpenses}
>
  clear expenses
</button>
