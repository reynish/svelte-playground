<script>
	export let name;
  import ChartLine from './Chart-line.svelte';
  
</script>

<main>
	<ChartLine style="border: 1px solid #333"></ChartLine>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	svg {
    border: 1px solid #333;
  }
  
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>