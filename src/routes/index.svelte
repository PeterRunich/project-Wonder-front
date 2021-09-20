<script context="module" lang="ts">
	import { plainToClass } from 'class-transformer';
	import { LinkUnit } from '../types/LinkUnit';
	import { TaskUnit } from '../types/TaskUnit';
	import TaskUnitIndex from '../components/task_units/TaskUnitIndex.svelte'
	import AllInWidget from '../components/link_units/AllInWidget.svelte'
	import DarkModeBtn from '../components/DarkModeBtn.svelte'
	import config from '../config'

	export async function load({ fetch }) {
		const date = new Date()
		const requests = []

		requests.push(fetch(config.origin + 'link_units?page=0&per_page=2'))
		requests.push(fetch(config.origin + `task_units?date=${date.getFullYear()}-${date.getMonth() + 1}-${date.getDate()}`))

		const response = await Promise.all(requests)
		if (response[0].ok && response[1].ok) {
			const link_units = await response[0].json()
			const tasks = await response[1].json()

			console.log(link_units, tasks)

			return {
						props: {
							link_units: link_units.data.map((link_unit) => plainToClass(LinkUnit, link_unit)),
							tasks: tasks.map((task) => plainToClass(TaskUnit, task))
						}
					}
		}
	}
</script>

<script lang="ts">
	export let link_units: LinkUnit[]
	export let tasks: TaskUnit[]
</script>

<DarkModeBtn/>

<div class='w-1/3 m-10'>
	<AllInWidget {link_units}/>
</div>
<div class='w-1/3 m-10'>
	<TaskUnitIndex {tasks}/>
</div>
