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

	function reloadWrapper() {location.reload();}
</script>

<h1 class="text-8xl text-center my-4 lowercase">jo</h1>
<h2 class="text-2xl text-center my-4">The <del>Trojan Asteroid</del> Light Curve App of Your Dreams</h2>

{#if isRunning}
	<button on:click={reloadWrapper}>Change settings nerd</button>
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
				observeeFile={settings.filename}
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
				observeeFile={settings.filename}
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
