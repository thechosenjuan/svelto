<script>
  export let task;
  export let index;
  export let id;
  export let deleteHandler = () => {};
  export let editHandler = () => {};

  let showIcons = false;
  let showEditBox = false;
  let inputValue = task;

  const handleMouseEnter = () => {
    showIcons = true;
  };
  const handleMouseLeave = () => {
    showIcons = false;
  };
  const handleDragStart = (e) => {
    showIcons = false;
    e.dataTransfer.setData("text/plain", e.target.id);
    e.dataTransfer.effectAllowed = "move";
  };

  const showEditBoxHandler = () => {
    showIcons = false;
    showEditBox = true;
  };
  const handleTaskEdit = (value) => {
    if (value.length > 0) {
      editHandler(index, value);
      showEditBox = false;
    }
  };
  const handleTaskDelete = (e) => {
    deleteHandler(index);
  };

  const handleCloseEditBox = () => {
    showEditBox = false;
  };
</script>

<div
  id={`task--${index}__list#${id}`}
  class="task__container"
  draggable="true"
  on:dragstart={handleDragStart}
  on:mouseenter={handleMouseEnter}
  on:mouseleave={handleMouseLeave}
>
  <div class="task__name">{task}</div>

  {#if showIcons}
    <div class="task__icons">
      <span class="icon__container" on:click={showEditBoxHandler}>
        <svg
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M15.2322 5.23223L18.7677 8.76777M16.7322 3.73223C17.7085 2.75592 19.2914 2.75592 20.2677 3.73223C21.244 4.70854 21.244 6.29146 20.2677 7.26777L6.5 21.0355H3V17.4644L16.7322 3.73223Z"
            stroke="#4A5568"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </span>
      <span class="icon__container" on:click={handleTaskDelete}>
        <svg
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M19 7L18.1327 19.1425C18.0579 20.1891 17.187 21 16.1378 21H7.86224C6.81296 21 5.94208 20.1891 5.86732 19.1425L5 7M10 11V17M14 11V17M15 7V4C15 3.44772 14.5523 3 14 3H10C9.44772 3 9 3.44772 9 4V7M4 7H20"
            stroke="#4A5568"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </span>
    </div>
  {/if}
  {#if showEditBox}
    <div>
      <input type="text" bind:value={inputValue} class="task-edit__input" />
      <button on:click={handleTaskEdit(inputValue)}>Edit</button>
      <button on:click={handleCloseEditBox}>Close</button>
    </div>
  {/if}
</div>

<style>
  .task__container {
    padding: 5px;
    font-size: 0.8rem;
    /* display: flex;
    justify-content: space-between; */
    min-height: 30px;
    border-bottom: 1px solid #888282d1;
  }
  .task__icons {
    display: block;
    float: right;
  }
  .task-edit__input {
    display: block;
  }
  .icon__container {
    display: inline-block;

    min-height: 24px;
    padding-left: 5px;
    padding-right: 5px;
    border-radius: 4px;
  }
  .icon__container:hover {
    cursor: pointer;
    background-color: aliceblue;
  }
  .task__name {
    margin-top: 5px;
    display: inline-block;
  }
</style>
