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
	<option value="1996hw1.obj">1996 Hw1</option>
	<option value="bacchus.obj">2068 Bacchus</option>
	<option value="castalia.obj">4769 Castalia</option>
	<option value="golevka.obj">6489 Golevka</option>
	<option value="hirestoutatis.obj">4179 Toutatis</option>
	<option value="Mithra.v1.PA.prograde.mod.obj">4486 Mithra</option>
	<option value="MKIII.obj">MKIII Spacesuit</option>
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
