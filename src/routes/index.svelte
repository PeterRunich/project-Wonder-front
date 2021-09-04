<script context="module" lang="ts">
	import { plainToClass } from 'class-transformer';
	import { LinkUnit } from '../types/LinkUnit';
	import AllInWidget from '../components/link_units/AllInWidget.svelte'
	import DarkModeBtn from '../components/DarkModeBtn.svelte'

	export async function load({ fetch }) {
		const res  = await fetch('http://localhost:3000/link_units?page=0&per_page=2')
		const data = await res.json()

		if (res.ok) {
			return { props: { link_units: data.data.map((link_unit) => plainToClass(LinkUnit, link_unit)) } }
		}
	}
</script>

<script lang="ts">
	export let link_units: LinkUnit[]
</script>


	<DarkModeBtn/>


<div class='w-1/3 m-10'>
	<AllInWidget {link_units}/>
</div>
