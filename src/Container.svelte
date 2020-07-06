<script>
  import Weather from "./Weather.svelte";
  import Analog from "./Analog.svelte";
  import Digital from "./Digital.svelte";
  import Date from "./Date.svelte";
  import Focus from "./Focus.svelte";
  import Shopping from "./Shopping.svelte";
  import Links from "./Links.svelte";

  let clicked = false;
  let analog = false;
  let input;
  let focus;

  const handleInput = e => {
    focus = input;
    input = "";
    let str = JSON.stringify(focus);
    localStorage.setItem("focus", str);
  };

  const storedFocus = localStorage.getItem("focus", focus);
  if (storedFocus) {
    focus = JSON.parse(storedFocus);
  }

  const switchClock = () => {
    analog = !analog;
  };
</script>

<style>
  nav {
    height: 4em;
  }
  form {
    height: 4em;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
  }

  .focus {
    padding: 10px;
    caret-color: rgb(209, 193, 193);
    text-align: left;
    font-family: "Poiret One", cursive;
    font-size: 2em;
    font-weight: bold;
    width: 100%;
    background: transparent;
    height: 2em;
    color: #fff;
  }
  .focus::placeholder {
    text-align: center;
    color: aliceblue;
  }
  .focus:focus {
    outline: none;
  }
</style>

<!-- NAVBAR -->
<nav class="bg1">
  <form on:submit|preventDefault={handleInput} autocomplete="off">
    <input
      bind:value={input}
      class="focus"
      name="focus"
      placeholder="What's your focus today?"
      type="text" />
  </form>
</nav>
<!-- GRID CONTAINER -->
<div class="container">
  <!--WEATHER-->
  <div id="weather" class="bg1">
    <Weather />
  </div>
  <!--TIME-->
  <div id="time" on:click={switchClock} class="bg1">
    {#if analog}
      <Analog />
    {:else}
      <Digital />
    {/if}
  </div>
  <!-- DATE -->
  <div id="date" class="bg2">
    <Date />
  </div>
  <!-- FOCUS -->
  <div id="focus" class="bg1">
    <Focus {focus} />
  </div>
  <!-- TODO LIST -->
  <div id="shopping" class="bg2">
    <Shopping />
  </div>
  <!-- TBD -->
  <div id="link" class="bg2">
    <Links />
  </div>
</div>
