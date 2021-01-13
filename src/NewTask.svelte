<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  let title, description, status;

  function buttonClick() {
    const task = {
      title,
      description,
      status,
    };
    dispatch("addTask", task);
  }
</script>

<div>
  <input type="text" bind:value={title} />
  <input type="text" bind:value={description} />
  <input type="text" bind:value={status} />
  <button on:click={buttonClick}>Add</button>
</div>
