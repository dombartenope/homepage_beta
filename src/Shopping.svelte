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
  .shopping-list {
    display: flex;
    flex-direction: column;
  }

  .item-add {
    text-align: center;
    padding: 10px;
    margin-bottom: 10px;
  }

  #name {
    border-radius: 4px;
    width: 80%;
  }

  li {
    list-style: none;
    margin-left: 20px;
    max-width: 70%;
    text-overflow: clip;
  }

  li button {
    border: none;
    background: transparent;
    padding: 1em;
    margin: 0;
  }

  li button:hover {
    transform: scale(1.1);
  }

  .done span {
    opacity: 0.4;
  }
</style>

<div class="shopping-list">
  <div class="item-add">
    <h1>
      Shopping List
      <i class="fa fa-clipboard-list" />
    </h1>

    <form on:submit|preventDefault={addItem} autocomplete="off">
      <label for="name">Add an item</label>
      <br />
      <input id="name" type="text" bind:value={name} />
    </form>
  </div>
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
