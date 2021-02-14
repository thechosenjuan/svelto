<script>
  import Task from "./Task.svelte";
  export let name;
  export let id;
  let showNewTaskForm = false;
  let taskName = "";
  let tasks = [];
  const handleListClick = () => {
    showNewTaskForm = true;
  };
  const handleAddTask = () => {
    tasks = [...tasks, taskName];
    taskName = "";
    showNewTaskForm = false;
  };
  const handleCloseTask = () => {
    showNewTaskForm = !showNewTaskForm;
  };

  const handleDragOver = (e) => {
    e.preventDefault();
    e.dataTransfer.dropEffect = "move";
  };

  const handleDrop = (e) => {
    e.preventDefault();
    const data = e.dataTransfer.getData("text/plain");
    e.currentTarget.appendChild(document.getElementById(data));
    // e.target.insertAdjacentElement("afterend", document.getElementById(data));
  };

  const updateTaskFromList = (index, newValue) => {
    tasks.splice(index, 1, newValue);
    tasks = tasks;
    // the function will be called from child - Task
    // I need to pass 2 ID's -> one for the task, one for the list
  };
  const deleteTaskFromList = (index) => {
    tasks.splice(index, 1);
    tasks = tasks;
  };
</script>

<div class="list" tabindex="0">
  <div class="list__name">
    {name}
  </div>

  <div
    class="drop-zone"
    on:dragover={handleDragOver}
    on:drop={handleDrop}
    id={`list--${id}`}
  >
    {#each tasks as task, index}
      <Task
        {task}
        {index}
        {id}
        editHandler={updateTaskFromList}
        deleteHandler={deleteTaskFromList}
      />
    {/each}
  </div>

  {#if showNewTaskForm}
    <div class="form-task__container">
      <form on:submit|preventDefault>
        <input type="text" bind:value={taskName} />
        <button on:click={handleAddTask}>Add card</button>
        <button on:click={handleCloseTask}>Close</button>
      </form>
    </div>
  {/if}
  <div on:click={handleListClick} class="list__add-card">Add a card</div>
</div>

<style>
  .list {
    /* padding: 10px 50px; */
    padding: 10px;
    background-color: #b9b5b5;
    border-radius: 4px;
    margin-right: 15px;
    display: inline-block;
    width: 250px;
    margin-bottom: 20px;
  }
  .list__name {
    font-weight: bold;
  }
  .form-task__container {
    display: inline-block;
    margin: 10px;
  }
  .list__add-card {
    font-size: 0.8rem;
    padding: 5px;
    cursor: pointer;
  }
  .list__add-card:hover {
    background-color: #959393;
  }
  /* .task__name:hover {
    background-color: #e3e3e3;
    cursor: pointer;
  } */
  .drop-zone {
    min-height: 20px;
    background-color: #a19ca1;
  }
  /* .task__icons {
    float: right;
    margin-top: -5px;
  } */
</style>
