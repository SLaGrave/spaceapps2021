<script>
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
</script>

<label for="filename">Select Object Model:</label>
<select name="filename" id="filename" bind:value={settings.filename}>
	<option value="kleo.obj">216 Kleopatra</option>
	<option value="betulia.obj">1580 Betulia</option>
	<option value="geographos.obj">1620 Geographos</option>
</select>

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
