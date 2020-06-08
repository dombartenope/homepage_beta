<script>
  import Weather from "./Weather.svelte";
  import Analog from "./Analog.svelte";
  import Digital from "./Digital.svelte";
  import Date from "./Date.svelte";

  let analog = true;
  const switchClock = () => {
    analog = !analog;
  };
</script>

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

  <div class="bg1" />
  <div class="bg1" />

  <div id="todo" class="bg2">TODO LIST</div>

  <!-- TODO: add two more bg2 divs -->
  <!-- TODO: add two long bg1 divs under todo list for "todo" and "complete" -->
</div>
