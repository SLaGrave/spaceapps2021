<script>
	import SimSettings from '../components/SimSettings.svelte';

	let settings;
</script>

<h1>Welcome to jo ¯\_(ツ)_/¯</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation.</p>
<br />
<SimSettings bind:settings />
<p>Test: {settings}</p>
