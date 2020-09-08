<script>
  import { slide } from "svelte/transition";

  export let list;
  export let toggleActive;
  export let showListType;
  export let removeItem;
  export let SHOW_LIST_TYPES;
</script>

<style>
  .completedList {
    margin-top: 20px;
    font-size: 1.2rem;
    display: flex;
    flex-direction: column;
  }

  .completedList .itemWrapper {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    margin-top: 10px;
  }

  .completedList .item {
    padding: 10px;
    display: flex;
    flex: 1;
    margin-right: 10px;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    height: 50px;
    border: 1px solid rgb(226, 226, 226);
    border-radius: 10px;
  }

  .completedList .item:hover {
    border: 1px solid rgb(97, 97, 255);
    cursor: pointer;
  }

  .completedList .itemWrapper .deleteButton {
    width: 60px;
    height: 50px;
    border-radius: 10px;
    background-color: rgb(255, 81, 203);
    color: white;
    font-size: 15px;
    text-align: center;
    padding-top: 12px;
  }

  .completedList .itemWrapper .deleteButton:hover {
    cursor: pointer;
  }
</style>

{#if showListType === SHOW_LIST_TYPES.COMPLETED}
  <div transition:slide class="completedList">
    {#each list as item}
      <div class="itemWrapper">
        <div class="item" on:click={() => toggleActive(item.id)}>
          <div>{item.text}</div>
        </div>
        <div class="deleteButton" on:click={() => removeItem(item.id)}>
          Delete
        </div>
      </div>
    {/each}
  </div>
{/if}
