<script>
	let observer_range = 0;
	let observer_period = 0;
    let observee_range = 0;
    let observee_period = 0;
</script>

<form><label>
    Observer Range
	<input type=number bind:value={observer_range} min=0><br>
    Observer Period
	<input type=number bind:value={observer_period} min=0><br>
    Observer Range
	<input type=number bind:value={observee_range} min=0><br>
    Observee Period
	<input type=number bind:value={observee_period} min=0><br>
</label></form>


