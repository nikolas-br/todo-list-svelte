<script>
  import NavElement from "./NavElement.svelte";
  export let showListType;
  export let changeShowListType;
  export let SHOW_LIST_TYPES;
</script>

<style>
  nav {
    border-bottom: 1px solid rgb(180, 180, 180);
  }

  nav ul {
    height: 35px;
    list-style: none;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
  }
</style>

<nav>
  <ul>
    <NavElement
      text={'All'}
      {showListType}
      {changeShowListType}
      index={SHOW_LIST_TYPES.ALL}
      underlineColor={'rgb(255, 81, 203)'} />

    <NavElement
      text={'Active'}
      {showListType}
      {changeShowListType}
      index={SHOW_LIST_TYPES.ACTIVE}
      underlineColor={'rgb(97, 97, 255)'} />

    <NavElement
      text={'Completed'}
      {showListType}
      {changeShowListType}
      index={SHOW_LIST_TYPES.COMPLETED}
      underlineColor={'rgb(226, 226, 226)'} />
  </ul>
</nav>
