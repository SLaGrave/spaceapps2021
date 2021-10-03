<script>
	export let settings = {
		observer_distance: 1,
		observer_period: 1,
		observee_distance: 2,
		observee_period: 0.5,
		vr: 360,
		xbound: 500,
		ybound: 500,
		filename: 'kleo.obj'
	};
</script>

<div class="w-full max-w-xs">
	<form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
		<label class="block text-gray-700 text-sm font-bold mb-2" for="filename"
			>Select Object Model:</label
		>
		<select name="filename" id="filename" bind:value={settings.filename}>
			<option selected="selected" value="kleo.obj">216 Kleopatra</option>
			<option value="betulia.obj">1580 Betulia</option>
			<option value="geographos.obj">1620 Geographos</option>
		</select>

		<label class="block text-gray-700 text-sm font-bold mb-2" for="observer_distance"
			>Observer Distance</label
		>
		<input
			name="observer_distance"
			type="number"
			bind:value={settings.observer_distance}
			min="0.1"
			max="Number.MAX_SAFE_INTEGER"
		/>AU
		<label class="block text-gray-700 text-sm font-bold mb-2" for="observer_distance"
			>Observer Period</label
		>
		<input
			name="observer_period"
			type="number"
			bind:value={settings.observer_period}
			min="0.1"
			max="Number.MAX_SAFE_INTEGER"
		/>
		years
		<label class="block text-gray-700 text-sm font-bold mb-2" for="observee_distance"
			>Observee Distance</label
		>
		<input
			name="observee_distance"
			type="number"
			bind:value={settings.observee_distance}
			min="0.1"
			max="Number.MAX_SAFE_INTEGER"
		/>
		AU
		<label class="block text-gray-700 text-sm font-bold mb-2" for="observee_period"
			>Observee Period</label
		>
		<input
			name="observee_period"
			type="number"
			bind:value={settings.observee_period}
			min="0.1"
			max="Number.MAX_SAFE_INTEGER"
		/>
		years
		<label class="block text-gray-700 text-sm font-bold mb-2" for="vr">Rotational Velocity</label>
		<input
			name="vr"
			type="number"
			bind:value={settings.vr}
			min="0.01"
			max="Number.MAX_SAFE_INTEGER"
		/>
		deg/day
		<label class="block text-gray-700 text-sm font-bold mb-2" for="xbound">Simulation xbound</label>
		<input name="xbound" type="number" bind:value={settings.xbound} min="200" max="2000" />
		pixels
		<label class="block text-gray-700 text-sm font-bold mb-2" for="ybound">Simulation ybound</label>
		<input name="ybound" type="number" bind:value={settings.ybound} min="200" max="2000" />
		pixels
	</form>
</div>
