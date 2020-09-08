<script>
  import { slide } from "svelte/transition";

  export let list;
  export let toggleActive;
  export let showListType;
  export let SHOW_LIST_TYPES;
</script>

<style>
  .list {
    margin-top: 20px;
    font-size: 1.2rem;
    display: flex;
    flex-direction: column;
  }

  .list .item {
    margin-top: 10px;
    padding: 10px;
    display: flex;
    /* flex-direction: row; */
    justify-content: space-between;
    align-items: center;
    height: 50px;
    border: 1px solid rgb(226, 226, 226);
    border-radius: 10px;
    overflow: hidden;
  }

  .list .itemCompleted {
    background-color: rgb(226, 226, 226);
    opacity: 0.3;
    color: black;
  }

  .list .item:hover {
    border: 1px solid rgb(97, 97, 255);
    cursor: pointer;
  }
</style>

{#if showListType === SHOW_LIST_TYPES.ACTIVE}
  <div transition:slide class="list">
    {#each list as item}
      <div
        class={item.isActive ? 'item' : 'item itemCompleted'}
        on:click={() => toggleActive(item.id)}>
        <div style={item.isActive ? '' : 'text-decoration: line-through'}>
          {item.text}
        </div>
      </div>
    {/each}
  </div>
{/if}
