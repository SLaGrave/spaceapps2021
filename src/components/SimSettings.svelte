<script>
    let files;
    export let _mythingamajig = {
        observer_range: 0,
        observer_period: 0,
        obervee_range: 0,
        observee_period: 0,
        filename: ""
    }
	

	$: if (files) {
		// Note that `files` is of type `FileList`, not an Array:
		// https://developer.mozilla.org/en-US/docs/Web/API/FileList
		console.log(files);

		for (const file of files) {
			alert(`${file.name}: ${file.size} bytes`);
		}
	}
    let simulation = { run: false };

    function toggle() {
        simulation.run = !simulation.run;
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
	<input type=number bind:value={_mythingamajig.observer_range} min=0 max=Number.MAX_SAFE_INTEGER> km<br>
    Observer Period
	<input type=number bind:value={_mythingamajig.observer_period} min=0 max=Number.MAX_SAFE_INTEGER> years<br>
    Observee Range
	<input type=number bind:value={_mythingamajig.observee_range} min=0 max=Number.MAX_SAFE_INTEGER> km<br>
    Observee Period
	<input type=number bind:value={_mythingamajig.observee_period} min=0 max=Number.MAX_SAFE_INTEGER> years<br>
</form>

{#if simulation.run}
	<button on:click={toggle}>
		Stop
	</button>
    <!-- Use to start sim with inputs. -->
{/if}

{#if !simulation.run}
	<button on:click={toggle}>
		Run
	</button>
    <!-- Use to kill sim. -->
{/if}