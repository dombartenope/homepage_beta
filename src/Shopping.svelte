<script>
  let items = [];

  const removeItem = item => {
    items = items.filter(i => i !== item);
    saveItems();
  };

  let name = "";

  const addItem = () => {
    items = [...items, { id: Math.random(), name, done: false }];
    name = "";
    saveItems();
  };

  //LOCAL STORAGE
  const saveItems = () => {
    const setStr = JSON.stringify(items);
    localStorage.setItem("items", setStr);
  };

  const getItems = () => {
    const getStr = localStorage.getItem("items");
    items = JSON.parse(getStr);
    if (!items) {
      items = [];
    }
  };
  getItems();
</script>

<style>
  #name {
    border-radius: 4px;
  }

  li {
    list-style: none;
  }

  li button {
    border: none;
    background: transparent;
    padding: 0;
    margin: 0;
  }

  li button:hover {
    transform: scale(1.1);
  }

  .done span {
    opacity: 0.4;
  }
</style>

<div>
  <h1>
    Shopping List
    <i class="fa fa-clipboard-list" />
  </h1>

  <form on:submit|preventDefault={addItem} autocomplete="off">
    <label for="name">Add an item</label>
    <br />
    <input id="name" type="text" bind:value={name} />
  </form>
  <ul>
    {#each items as item}
      <li class:done={item.done}>
        <input type="checkbox" bind:checked={item.done} />
        <span>{item.name}</span>
        <button on:click={() => removeItem(item)}>❌</button>
      </li>
    {/each}
  </ul>
</div>
