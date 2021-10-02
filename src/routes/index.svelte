<script>
	import ThreeSimulation from '../components/ThreeSimulation.svelte';
	import ThreeVisualizer from '../components/ThreeVisualizer.svelte';

    let ll = 420.69;
</script>

<h1>I Forgor 💀</h1>

<h2>Light Level: {ll}</h2>

<div class="row">
    <div class="column">
        <ThreeSimulation width={500} height={500} bind:lightLevel={ll} />
    </div>
    <div class="column">
        <ThreeVisualizer width={500} height={500} />
    </div>
    <div class="column">
        Nate's settings component
    </div>
    <div class="column">
        Edwin's graph component
    </div>
</div>

<style>
	.row {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		width: 100%;
	}

	.column {
		display: flex;
		flex-direction: column;
		flex-basis: 100%;
		flex: 1;
	}
</style>
