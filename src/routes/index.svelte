<script>
	import SimSettings from '../components/SimSettings.svelte';
	import ThreeSimulation from '../components/ThreeSimulation.svelte';
	import ThreeVisualizer from '../components/ThreeVisualizer.svelte';
	import ChartJsPlot from '../components/ChartJSPlot.svelte';

	let settings;
	let lightLevel = 420.69;
	let lightLevelArray;

	// State tracking
	let isRunning = false;
	function toggleRunning() {
		console.log(settings);
		isRunning = true;
	}

	function reloadWrapper() {
		location.reload();
	}
</script>

<h1 class="text-8xl text-center my-4 lowercase">jo</h1>
<h2 class="text-2xl text-center my-4">
	The <del>Trojan Asteroid</del> Light Curve App of Your Dreams
</h2>

{#if isRunning}
	<div class="my-12 flex flex-col items-center">
		<button
			on:click={reloadWrapper}
			class="my-4 bg-green-400 hover:bg-green-600 text-white font-bold py-2 px-4 rounded"
			>Change Settings</button
		>
		<div class="mx-12 flex flex-row items-center">
			<ThreeSimulation
				width={settings.xbound}
				height={settings.ybound}
				observerDistance={settings.observer_distance}
				observerOrbitalPeriod={settings.observer_period}
				observeeDistance={settings.observee_distance}
				observeeOrbitalPeriod={settings.observee_period}
				observeeObjScale={settings.observee_scale}
				observeeRotationVelocity={settings.vr}
				observeeFile={settings.filename}
				bind:lightLevel
				bind:lightLevelArray
			/>
			<ThreeVisualizer
				width={settings.xbound}
				height={settings.ybound}
				observerOrbitalPeriod={settings.observer_period}
				observeeOrbitalPeriod={settings.observee_period}
				observeeObjScale={settings.observee_scale}
				observeeRotationVelocity={settings.vr}
				observeeFile={settings.filename}
				bind:lightLevel
			/>
		</div>
		<ChartJsPlot inputData={lightLevelArray} />
	</div>
{:else}
	<div class="my-12 flex flex-col items-center">
		<div class="max-w-md bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
			<i>jo</i> is an application which allows users to explore the shape, distance, and orbital
			period of an object such as an asteroid effect its light curve. More information on light
			curves and this project as a whole can be found on our <a class="underline text-blue-600 hover:text-blue-800 visited:text-purple-600" href="/about">about page</a>.
		</div>
		<SimSettings bind:settings />
		<button
			on:click={toggleRunning}
			class="bg-green-400 hover:bg-green-600 text-white font-bold py-2 px-4 rounded"
			>Run Simulation</button
		>
	</div>
{/if}
