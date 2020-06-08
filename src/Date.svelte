<script>
  import moment from "moment";
  //formats dates via moment
  const date = moment().format("MMMM Do");
  const year = moment().format("YYYY");
  const day = moment().format("d");
  //Stores week days in array to be printed on screen
  const week = ["S", "M", "T", "W", "T", "F", "S"];
  //Allows for 'today' to be replaced daily and highlighted
  let beforeToday = week.slice(0, day);
  let today = week[day];
  let afterToday = week.slice(day, week.length);
  //Removes double days when printing to the screen
  if (afterToday[0] === week[day]) {
    afterToday.shift();
  }
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
  {afterToday
    .toString()
    .split(',')
    .join(' ')}
</p>
