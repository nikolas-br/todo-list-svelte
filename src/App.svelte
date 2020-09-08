<script>
  import { fade } from "svelte/transition";

  import Navigation from "./Navigation.svelte";
  import AllList from "./AllList.svelte";
  import ActiveList from "./ActiveList.svelte";
  import CompletedList from "./CompletedList.svelte";
  import MyWebStorageAPI from "./webStorageAPI";
  import { onMount } from "svelte";

  const myWebStorage = new MyWebStorageAPI();

  const SHOW_LIST_TYPES = { ALL: 0, ACTIVE: 1, COMPLETED: 2 };

  const demoEntries = [
    { text: "Buy chocolate", isActive: true, id: 0 },
    { text: "Quit slacking", isActive: false, id: 1 },
    { text: "Write toDo app", isActive: false, id: 2 },
    { text: "Do 15 laps around the block", isActive: true, id: 3 },
    { text: "Cook delicious meal", isActive: true, id: 4 },
  ];

  let showListType = SHOW_LIST_TYPES.ALL;
  let list = demoEntries;
  let entry = "";

  onMount(() => {
    const storedList = myWebStorage.getList();
    if (!storedList.length) return;

    list = storedList;
  });

  const changeShowListType = (type) => {
    showListType = type;
  };

  const toggleActive = (id) => {
    list.forEach((item) => {
      if (item.id === id) item.isActive = !item.isActive;
    });
    list = list;
    myWebStorage.saveList(list);
  };

  const removeItem = (id) => {
    list = list.filter((item) => item.id !== id);
    myWebStorage.saveList(list);
  };

  const addEntry = () => {
    list = [
      ...list,
      { text: entry, isActive: true, id: entry + Math.random() },
    ];
    entry = "";
    myWebStorage.saveList(list);

    if (showListType == SHOW_LIST_TYPES.COMPLETED)
      showListType = SHOW_LIST_TYPES.ACTIVE;
  };
</script>

<style>
  :global(*) {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
    font-family: "Poppins", sans-serif;
    color: rgb(78, 78, 78);
  }

  .App {
    max-width: 520px;
    margin: auto;
    margin-top: 100px;
    padding: 20px;
  }

  header {
    font-size: 3rem;
    text-align: center;
    font-style: italic;
    margin-bottom: 50px;
  }

  header h2 {
    background: -webkit-linear-gradient(
      30deg,
      rgb(97, 97, 255),
      rgb(255, 81, 203)
    );
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  form {
    margin-top: 20px;
    width: 100%;
    display: flex;
    justify-content: space-between;
  }

  form input {
    width: 100%;
    height: 40px;
    font-size: 1rem;
    padding-left: 10px;
    border-radius: 10px;
    margin-right: 10px;
    color: rgb(97, 97, 255);
    font-style: italic;
    border: 1px solid grey;
  }

  form input:focus {
    outline: none;
  }

  form button {
    width: 60px;
    height: 40px;
    border-radius: 10px;
    border: none;
    background-color: rgb(97, 97, 255);
    color: white;
    font-size: 1.5rem;
    padding: 0;
  }

  form button:focus {
    outline: none;
  }

  form button:hover {
    cursor: pointer;
  }

  .blogLink {
    display: flex;
    justify-content: center;
    margin-top: 200px;
    margin-bottom: 400px;
  }

  @media only screen and (max-width: 500px) {
    .App {
      margin-top: 20px;
    }
  }
</style>

<svelte:head>
  <link
    href="https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,300;0,400;0,500;1,300;1,400;1,500&display=swap"
    rel="stylesheet" />
</svelte:head>

<div class="App">
  <header>
    <h2>#toDo</h2>
  </header>

  <Navigation {showListType} {changeShowListType} {SHOW_LIST_TYPES} />

  <form on:submit|preventDefault={addEntry}>
    <input
      on:change={(e) => {
        entry = e.target.value;
      }}
      value={entry} />
    <button type="submit">+</button>
  </form>

  <AllList {list} {toggleActive} {showListType} {SHOW_LIST_TYPES} />

  <ActiveList
    list={list.filter((item) => item.isActive)}
    {toggleActive}
    {showListType}
    {SHOW_LIST_TYPES} />

  <CompletedList
    list={list.filter((item) => !item.isActive)}
    {toggleActive}
    {removeItem}
    {showListType}
    {SHOW_LIST_TYPES} />

  <a class="blogLink" href="https://www.nikolas-blog.com"> nikolas-blog.com </a>
</div>
