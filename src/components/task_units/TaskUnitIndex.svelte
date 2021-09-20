<script lang="ts">
    import { TaskUnit } from '../../types/TaskUnit'
    import config from '../../config'

    export let tasks: TaskUnit[]

    async function checkboxChanged(e, task: TaskUnit) {
        e.preventDefault()
        task.is_completed = !task.is_completed

        const data = JSON.stringify({ is_completed: task.is_completed })

        await fetch(config.origin + `task_units/${task.id}`,
            {
                method: "PUT",
                body: data,
                headers: { 'Content-Type': 'application/json' }
            })
    }
</script>

{#each tasks as task, index (task.id)}
    <p>{`${index}. ${task.title}`}</p>
    <input on:change={(e)=>checkboxChanged(e, task)} type="checkbox" checked={task.is_completed}/>
{/each}
