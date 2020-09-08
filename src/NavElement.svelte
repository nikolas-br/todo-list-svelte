<script>
  export let text;
  export let showListType;
  export let changeShowListType;
  export let index;
  export let underlineColor;
</script>

<style>
  * {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
    font-family: "Poppins", sans-serif;
  }

  li {
    width: 100px;
    text-align: center;
    font-weight: 500;
  }

  li:hover {
    border-bottom: 5px solid rgb(226, 226, 226);
    margin-bottom: -5px;
    cursor: pointer;
  }
</style>

<li
  on:click={() => changeShowListType(index)}
  style={showListType !== index ? '' : `border-bottom: 5px solid ${underlineColor}; margin-bottom: -5px`}>
  {text}
</li>
