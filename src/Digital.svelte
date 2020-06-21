<script>
  import moment from "moment";
  import { onMount } from "svelte";

  let date = moment().format("hh: mm: ss");
  let dayNight = moment().format("A");

  onMount(() => {
    const interval = setInterval(() => {
      date = moment().format("hh: mm: ss");
      dayNight = moment().format("A");
      //   icon = hour >= 12 ? "fa fas sunny" : "fa fas sunny";
    }, 1000);
  });
</script>

<style>
  * {
    cursor: pointer;
  }
  @media only screen and (max-width: 740px) {
    h1 {
      font-size: 1em;
    }
  }
</style>

<h1>{date}</h1>
<h3>{dayNight}</h3>
