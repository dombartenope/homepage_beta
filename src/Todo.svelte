<script>
  import { slide } from "svelte/transition";
  import { elasticInOut } from "svelte/easing";

  let todos = [];
  let input = "";

  function addTodo() {
    if (input)
      todos = [
        ...todos,
        {
          text: input,
          id: Math.random()
            .toString(36)
            .substr(2, 9)
        }
      ];
    input = "";
  }

  function removeTodo(id) {
    const index = todos.findIndex(todo => todo.id === id);
    todos.splice(index, 1);
    todos = todos;
  }
</script>

<style>
  h1 {
    text-align: center;
    font-size: 3em;
  }

  input {
    width: 20em;
    font-size: 1em;
    font-weight: bold;
    font-family: Poiret One;
    border-radius: 4px;
    height: 40px;
  }

  input::placeholder {
    text-align: center;
  }

  button {
    border-radius: 50%;
    background: rgb(51, 233, 51);
    outline: none;
    border: 0.5px solid green;
    box-shadow: -1px 0px 2px 0px black;
  }
  button:focus {
    outline: none;
  }

  i {
    margin-top: 5px;
    width: 1.85em;
    height: 1rem;
    display: inline-block;
  }

  li {
    text-align: center;
    font-size: 2em;
    list-style: none;
  }
</style>

<div class="box">
  <div class="todolist">
    <h1>
      Todo List
      <span>
        <i class="fas fa-clipboard-list" />
      </span>
    </h1>
    <form style="justify-content: center" on:submit|preventDefault={addTodo}>
      <div class="control">
        <input
          bind:value={input}
          class="input"
          type="text"
          placeholder="TODO" />

        <button>
          <span>
            <i class="fas fa-plus" />
          </span>
        </button>
      </div>
    </form>
    <ul class:list={todos.length > 0}>
      {#each todos as todo (todo.id)}
        <li
          class="list-item"
          transition:slide={{ duration: 300, easing: elasticInOut }}>
          <div style="align-items: center">
            <span>{todo.text}</span>
            <button on:click={() => removeTodo(todo.id)}>
              <span class="icon">
                <i class="fas fa-check" />
              </span>
            </button>
          </div>
        </li>
      {:else}
        <li
          transition:slide={{ delay: 600, duration: 300, easing: elasticInOut }}>
          Nothing here!
        </li>
      {/each}
    </ul>
  </div>
</div>
