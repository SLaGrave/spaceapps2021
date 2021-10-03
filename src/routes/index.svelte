<script>
	import SimSettings from '../components/SimSettings.svelte';
	import ThreeSimulation from '../components/ThreeSimulation.svelte';
	import ThreeVisualizer from '../components/ThreeVisualizer.svelte';
	import ChartJsPlot from '../components/ChartJSPlot.svelte';

	let settings;
	let lightLevel = 420.69;
	let lightLevelArray

	// State tracking
	let isRunning = false;
	function toggleRunning() {
		console.log(settings);
		isRunning = true;
	}
</script>

<h1>jo</h1>
<h2>The Asteroid App of Your Dreams</h2>

{#if isRunning}
	<div class="row">
		<div class="column">
			<ThreeSimulation
				width={settings.xbound}
				height={settings.ybound}
				observerDistance={settings.observer_distance}
				observerOrbitalPeriod={settings.observer_period}
				observeeDistance={settings.observee_distance}
				observeeOrbitalPeriod={settings.observee_period}
				observeeRotationVelocity={settings.vr}
				observeeSTLFile={settings.filename}
				bind:lightLevel
				bind:lightLevelArray
			/>
		</div>
		<div class="column">
			<ThreeVisualizer
				width={settings.xbound}
				height={settings.ybound}
				observerDistance={settings.observer_distance}
				observerOrbitalPeriod={settings.observer_period}
				observeeDistance={settings.observee_distance}
				observeeOrbitalPeriod={settings.observee_period}
				observeeRotationVelocity={settings.vr}
				bind:lightLevel
			/>
		</div>
	</div>
	<div class="row">
		<div class="column">
			<ChartJsPlot inputData={lightLevelArray} />
		</div>
	</div>	


{:else}

	<SimSettings bind:settings />
	<button on:click={toggleRunning}>Run Simulation</button>

{/if}

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
