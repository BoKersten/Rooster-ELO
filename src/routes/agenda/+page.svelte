<head>
	<title>Agenda</title>
</head>

<script>
	import Calendar from "../../lib/components/Calendar.svelte";
	import DayCalendar from "../../lib/components/DayCalendar.svelte";
	let calendarMode = "day";

	$: console.log(calendarMode);
</script>

<main>
	<select bind:value={calendarMode} class="select w-full max-w-xs">
		<option disabled select>Weergave</option>
		<option value="month">maand</option>
		<option value="day">dag</option>
	</select>
	{#if calendarMode == "month"}
	<Calendar/>
	{/if}
	{#if calendarMode == "day"}
		 <DayCalendar/>
	{/if}
	
</main>