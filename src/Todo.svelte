<script>
  let todos = [];

  const removeItem = item => {
    todos = todos.filter(i => i !== item);
    saveItems();
  };

  let todo = "";

  const addItem = () => {
    todos = [...todos, { id: Math.random(), todo, done: false }];
    todo = "";
    saveItems();
  };

  //LOCAL STORAGE
  const saveItems = () => {
    const setStr = JSON.stringify(todos);
    localStorage.setItem("todos", setStr);
  };

  const getItems = () => {
    const getStr = localStorage.getItem("todos");
    todos = JSON.parse(getStr);
    if (!todos) {
      todos = [];
    }
  };

  getItems();
</script>

<style>
  .todo-list {
    display: flex;
    flex-direction: column;
  }

  .item-add {
    text-align: center;
    padding: 10px;
    margin-bottom: 10px;
  }

  #todo {
    margin-top: 10px;
    font-size: 1.5em;
    border-radius: 4px;
    width: 80%;
    height: 2em;
  }

  h1 {
    margin-bottom: 10px;
  }

  @media only screen and (max-width: 740px) {
    li {
      font-size: 1rem;
    }
  }

  li {
    font-size: 1.5em;
    list-style: none;
    margin-left: 20px;
    max-width: 90%;
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
    opacity: 0.6;
  }
</style>

<div class="todo-list">
  <div class="item-add">
    <h1>
      Todo List
      <i class="fa fa-clipboard-list" />
    </h1>

    <form on:submit|preventDefault={addItem} autocomplete="off">
      <label for="todo">Add an item</label>
      <br />
      <input id="todo" type="text" bind:value={todo} />
    </form>
  </div>
  <ul>
    {#each todos as item}
      <li class:done={item.done}>
        <input id="check" type="checkbox" bind:checked={item.done} />
        <span>{item.todo}</span>
        <button on:click={() => removeItem(item)}>❌</button>
      </li>
    {/each}
  </ul>
</div>
