<script>
	let files;

	export let settings = {
		observer_distance: 1,
		observer_period: 1,
		observee_distance: 2,
		observee_period: 0.5,
		vr: 360,
		xbound: 500,
		ybound: 500,
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
	Observer Distance
	<input
		type="number"
		bind:value={settings.observer_distance}
		min="0.1"
		max="Number.MAX_SAFE_INTEGER"
	/>
	AU<br />
	Observer Period
	<input
		type="number"
		bind:value={settings.observer_period}
		min="0.1"
		max="Number.MAX_SAFE_INTEGER"
	/>
	years<br />
	Observee Distance
	<input
		type="number"
		bind:value={settings.observee_distance}
		min="0.1"
		max="Number.MAX_SAFE_INTEGER"
	/>
	AU<br />
	Observee Period
	<input
		type="number"
		bind:value={settings.observee_period}
		min="0.1"
		max="Number.MAX_SAFE_INTEGER"
	/>
	years<br />
	Rotational Velocity
	<input type="number" bind:value={settings.vr} min="0.01" max="Number.MAX_SAFE_INTEGER" />
	deg/earth day<br />
	Simulation xbound:
	<input type="number" bind:value={settings.xbound} min="200" max="2000" />
	pixels<br />
	Simulation ybound
	<input type="number" bind:value={settings.ybound} min="200" max="2000" />
	pixels<br />
</form>
