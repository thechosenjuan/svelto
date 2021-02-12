<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  function addListClick() {
    dispatch("addNewList");
  }

  // let key;
  // let keyCode;

  // const handleButtonFocus = () => {
  //   console.log('im being focused')
  // }
  // const handleEnterPress = (event) =>{
  //   key = event.key;
  //   keyCode = event.keyCode
  // }
</script>

<span class="add-new-list__button" on:click={addListClick} tabindex="0"
  >Add List +</span
>

<style>
  .add-new-list__button {
    padding: 10px;
    background-color: #e3e1e1;
    border-radius: 4px;
    cursor: pointer;
  }
</style>
