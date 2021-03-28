<script>
  import { getContext } from 'svelte';
    
  const clearExpenses = getContext('remove');
</script>

<button type="button" class="btn btn-primary btn-block" on:click="{clearExpenses}">
    clear expenses
</button>