<script>
	let subcategory = ''
	let description = ''
	const current_time = (new Date()).toISOString().slice(0, -8)
	export let end_time = current_time
	export let goes_through_present
	$: goes_through_present = (end_time == current_time)
	export let start_time
	let subcategories = ['a','b','Driving to store']
	let categories = ['good','bad','neutral']
	$: valid_end_time = (end_time > start_time) && !(end_time > current_time)
	$: if (subcategory == "+ NEW SUBCATEGORY") {
		let new_subcategory = prompt('Enter a subcategory name')
		let new_category = prompt('CURRENT CATEGORIES\n' + categories.join('\n') +
														 '\nPlease enter a new category')
		subcategories.push(new_subcategory)
		categories.push(new_category)
		subcategory = new_subcategory
		//Push new subcategories to cache ##TODO
		//Push new subcategory-category pairs to server
	}
</script>
What were you doing at
<input type= "datetime-local" bind:value={start_time} disabled=true style:color='black'
			 style:background-color='magenta'>
<b style:font-size=24px>?&nbsp;&nbsp;</b>
<select name='subcategory' bind:value={subcategory}>
	<option></option>
	<option>+ NEW SUBCATEGORY</option>
	{#each subcategories as sub, i}
	<option>{sub}</option>
	{/each}
</select>
<input type="text" bind:value={description} placeholder='description'>
<input type= "datetime-local" bind:value={end_time} placeholder='end_time'
			 style:border-color={valid_end_time ? 'black' : 'red'}
			 style:border-width={valid_end_time ? '1px' : '6px'}>
<p>
	{goes_through_present}{start_time}
</p>
