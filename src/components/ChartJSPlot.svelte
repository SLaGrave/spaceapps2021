<script>
	import { onMount } from 'svelte';
	import Chart from 'chart.js/auto/auto.js';

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
						backgroundColor: 'rgba(52, 211, 153, 1)',
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

<div class="mx-12 flex flex-col items-center bg-blue-100 shadow-md rounded px-8 pt-6 pb-8 mb-4">
	<button
		class="my-4 bg-green-400 hover:bg-green-600 text-white font-bold py-2 px-4 rounded"
		on:click={reloadGraph}>Reload <b>Light Curve</b> graph</button
	>
	This graph shows how the amount of light reflected off the observed object changes with the two object's
	relative position.
	<canvas id="myChart" width="500" height="500" />
</div>
