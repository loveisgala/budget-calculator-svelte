<style>
  .expense {
    display: flex;
    align-items: center;
  }

  .expense-index {
    margin-right: 1rem;
  }
</style>

<script>
  export let index;
  export let expense;
  let { name, amount, id } = expense;
</script>

<div class="expense">
  <p class="expense-index">{index}</p>
  <h2>title: {name}</h2>
  <h2>amount: {amount}</h2>
</div>

