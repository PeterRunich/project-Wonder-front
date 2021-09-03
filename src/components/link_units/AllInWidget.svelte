<script lang="ts">
	import { LinkUnit} from '../../types/LinkUnit';

	export let link_units: LinkUnit
</script>

<h3 class='text-2xl mb-2'>Ссылки</h3>
<ul class='shadow-lg rounded-lg p-3.5 divide-y divide-gray-200'>
	{#each link_units as link_unit}
		<li class='my-2'>
			<a class='underline text-red-400' href={link_unit.url}>{link_unit.url}</a>
			<p>Заметка: {link_unit.note}</p>
		</li>
	{/each}
</ul>


