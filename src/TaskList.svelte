<script>
    import Task from "./Task.svelte";
    let tasks = [];
</script>

<div>
    {#each tasks as task}
        <Task title={task.title} description={task.description} status={task.status}/>
    {/each}
</div>
