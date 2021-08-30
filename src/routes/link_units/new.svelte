<script lang="ts">
	let form_data, url, note: string

	$: form_data = {'link_unit': { 'url': url, 'note': note} }

	async function formHandler(event: Event) {
		event.preventDefault()

		const response = await fetch('http://localhost:3000/link_units', { method: 'POST', headers: { 'Content-Type': 'application/json;charset=utf-8' }, body: JSON.stringify(form_data)})
		alert(response.status)
	}
</script>

<form on:submit={formHandler} name='link_unit'>
	<input bind:value={url} type='text' placeholder='link' name='url'/>
	<input bind:value={note} type='text' placeholder='note' name='note'/>
	<input type='submit'>
</form>
