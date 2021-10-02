<script>
	import { onMount } from 'svelte';
	import Chart from 'chart.js/auto';

	export let inputData = [12, 19, 3, 5, 2, 3];

	let ctx;
	let myChart;
	let range = (n) => Array.from(Array(n).keys());

	onMount(() => {
		reloadGraph();
	});

	function reloadGraph() {
		if (myChart) myChart.destroy();

		ctx = document.getElementById('myChart').getContext('2d');
		myChart = new Chart(ctx, {
			type: 'scatter',
			data: {
				labels: range(inputData.length),
				datasets: [
					{
						label: 'Light Curve',
						data: inputData,
						backgroundColor: 'rgba(255, 99, 132, 0.2)',
						borderWidth: 1
					}
				]
			},
			options: {
				maintainAspectRatio: true,
				responsive: false,
				scales: {
					y: {
						title: {
							display: true,
							text: 'observed light level (total rgb value of simulation)'
						}
					},
					x: {
						title: {
							display: true,
							text: 'time (frames)'
						}
					}
				}
			}
		});
	}
</script>


<button on:click={reloadGraph}>Reload <b>Light Curve</b> graph</button>

<canvas id="myChart" width="500" height="500" />
