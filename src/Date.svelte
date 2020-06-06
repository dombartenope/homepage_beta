<script>
  import moment from "moment";

  const date = moment().format("MMMM Do");
  const year = moment().format("YYYY");
  const day = moment().format("d");

  const week = ["S", "M", "T", "W", "T", "F", "S"];
  let beforeToday = week.slice(0, day);
  let today = week[day];
  let afterToday = week.slice(day, week.length);
</script>

<style>
  .today {
    font-size: 1.3em;
    color: white;
  }
</style>

<h1>{date}</h1>
<h2>{year}</h2>
<p>
  {beforeToday
    .toString()
    .split(',')
    .join(' ')}
  <span class="today">{today}</span>
  {#if day < 6}
    {afterToday
      .toString()
      .split(',')
      .join(' ')}
  {/if}
</p>
