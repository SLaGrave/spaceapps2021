<script>
	let files;

	export let settings = {
		observer_range: 0,
		observer_period: 0,
		obervee_range: 0,
		observee_period: 0,
		vr: 0,
		xbound: 0,
		ybound: 0,
		filename: ''
	};

	$: if (files) {
		// Note that `files` is of type `FileList`, not an Array:
		// https://developer.mozilla.org/en-US/docs/Web/API/FileList
		console.log(files);

		for (const file of files) {
			alert(`${file.name}: ${file.size} bytes`);
			settings['filename'] = file.name;
		}
	}
</script>

<label for="avatar">Upload STL File:</label>
<input accept=".stl" bind:files id="avatar" name="avatar" type="file" />

{#if files}
	<h2>Selected files:</h2>
	{#each Array.from(files) as file}
		<p>{file.name} ({file.size} bytes)</p>
	{/each}
{/if}

<form>
	Observer Range
	<input type="number" bind:value={settings.observer_range} min="0" max="Number.MAX_SAFE_INTEGER" />
	km<br />
	Observer Period
	<input
		type="number"
		bind:value={settings.observer_period}
		min="0"
		max="Number.MAX_SAFE_INTEGER"
	/>
	years<br />
	Observee Range
	<input type="number" bind:value={settings.observee_range} min="0" max="Number.MAX_SAFE_INTEGER" />
	km<br />
	Observee Period
	<input
		type="number"
		bind:value={settings.observee_period}
		min="0"
		max="Number.MAX_SAFE_INTEGER"
	/>
	years<br />
	Rotational Velocity
	<input type="number" bind:value={settings.vr} min="0" max="Number.MAX_SAFE_INTEGER" />
	deg/frame<br />
	Simulation xbound:
	<input type="number" bind:value={settings.xbound} min="0" max="202000" />
	pixels<br />
	Simulation ybound
	<input type="number" bind:value={settings.ybound} min="0" max="202000" />
	pixels<br />
</form>

<button on:click={console.log(settings)}> Run </button>
