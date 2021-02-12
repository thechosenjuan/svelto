<script>
  // import NewTask from "./NewTask.svelte";
  // import TaskList from "./TaskList.svelte";
  import AddNewList from "./AddNewList.svelte";
  import List from "./List.svelte";

  let showNewListForm = false;

  let listName = "";

  let listsArray = [];

  const handleAddNewList = () => {
    showNewListForm = true;
  };
  const handleButtonClick = () => {
    listsArray =
      listName.length > 0 ? [...listsArray, listName] : [...listsArray];
    listName = "";
    showNewListForm = false;
  };
</script>

<main>
  <!-- <NewTask on:addTask={addTaskHandler} /> -->
  <!-- <TaskList /> -->

  <!--Renderear arreglo de listas-->

  <!--AQUI DEBE DE IR EL DROP ZONE-->
  {#each listsArray as list, index}
    <List name={list} id={index} />
  {/each}
  {#if !showNewListForm}
    <AddNewList on:addNewList={handleAddNewList} />
  {:else}
    <div class="form-list__container">
      <form on:submit|preventDefault>
        <input type="text" bind:value={listName} />
        <button on:click={handleButtonClick} tabindex="0">Add List</button>
      </form>
    </div>
  {/if}
</main>

<style>
  main {
    padding: 40px;
  }
  .form-list__container {
    display: inline-block;
  }
</style>
