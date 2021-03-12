<script>
	//Components
	import Navbar from './components/Navbar.svelte';
	import expensesData from './expenses';
	import ExpensesList from './ExpensesList.svelte';

	//Variables
	let expenses = [...expensesData];

</script>

<Navbar/>
<main class="content">
	<ExpensesList expenses={expenses}/>
</main>
