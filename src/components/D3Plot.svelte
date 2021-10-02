<head>
    <script src="https://d3js.org/d3.v4.min.js"></script>
</head>

<script>
	import { onMount } from 'svelte';
	import * as d3 from 'd3';
	

	/*create a random dataset of floats*/
	var data = []
	for (let i = 0; i < 20; i++) {
		data[i] = Math.round(Math.random()*200_000) / 1000;
	}

	let el;

	onMount(() => {
		d3.select(el)           /*Select the DOM element (chart) bound to el*/
			.selectAll("div")   /*Select all "div" css sections within the chart*/
			.data(data)
			.enter()
			.append("div")
			.style("width", function(d) {
				return (d*2) + "px";
			})
			.text(function(d) {
				return "Value " + d;
			});
	});
</script>

<style>
	.chart :global(div) {       /*chart is the name of the graph style*/
		font: 1px sans-serif;
		background-color: rgb(116, 199, 116);
		text-align: right;
		padding: 0px;
		margin: 0px;
		color: white;
	}
</style>

<div bind:this={el} class="chart"></div>