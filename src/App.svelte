<script>
  import NewTask from "./NewTask.svelte";
  import TaskList from "./TaskList.svelte";
  const addTaskHandler = (e) => {
    console.log(e.detail);
  };
</script>

<main>
  <NewTask />
  <TaskList on:addTask={addTaskHandler} />
</main>
