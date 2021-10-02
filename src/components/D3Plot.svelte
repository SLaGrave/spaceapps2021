<head>
    <script src="https://d3js.org/d3.v4.min.js"></script>
</head>

<script>
	import { onMount } from 'svelte';
	import * as d3 from 'd3';
	var data = [30, 86, 168, 281, 303, 365];
	
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
				return d;
			});
	});
</script>

<style>
	.chart :global(div) {       /*chart is the name of the graph style*/
		font: 10px sans-serif;
		background-color: steelblue;
		text-align: right;
		padding: 3px;
		margin: 1px;
		color: white;
	}
</style>

<div bind:this={el} class="chart"></div>