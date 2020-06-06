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

  <div class="bg1">
    <Weather />
  </div>

  <div on:click={switchClock} class="bg1">
    {#if analog}
      <Analog />
    {:else}
      <Digital />
    {/if}
  </div>

  <div class="bg2">
    <h2>
      <i class="fas fa-running" />
    </h2>
    <p>Miles</p>
  </div>

  <div class="bg1">Test</div>

  <div class="bg1">
    <h2>
      <i class="fas fa-bed" />
    </h2>
    <p>Sleep Keep</p>
  </div>

  <div class="bg2">
    <Date />
  </div>

  <div class="bg1">
    <h2>
      170
      <span>lbs</span>
    </h2>
    <p>Weight</p>
  </div>

  <div class="bg1">
    <h2>
      28
      <span>%</span>
    </h2>
    <p>Fat Percentage</p>
  </div>

  <div class="bg2">
    <h2>
      118
      <span>mgdl</span>
    </h2>
    <p>Blood Glucose</p>
  </div>

  <div class="bg2">
    <h2>
      680
      <span>kcal</span>
    </h2>
    <p>AVG Consumption</p>
  </div>

  <div class="bg2">TEST</div>

  <div class="bg2">
    <h2>
      85
      <span>%</span>
    </h2>
    <p>Body Hydration</p>
  </div>

</div>
