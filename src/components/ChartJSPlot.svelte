<script>
	import { onMount } from 'svelte';
	export let inputData = [12, 19, 3, 5, 2, 3];

	let range = (n) => Array.from(Array(n).keys());

	onMount(() => {
		let myChart = new Chart('myChart', {
			type: 'scatter',
			data: {
				labels: range(inputData.length),
				datasets: [
					{
						label: '# of Votes',
						data: inputData,
						borderWidth: 1
					}
				]
			},
			options: {
				scales: {
					y: {
						beginAtZero: true
					}
				}
			}
		});
	});
</script>

<svelte:head>
	<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</svelte:head>

<canvas id="myChart" width="400" height="400" />
