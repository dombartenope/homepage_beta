<script>
  import axios from "axios";

  let location;
  let desc;
  let temp;
  let icon;
  let incomeData = null;
  let loading = true;
  let celcius;
  if (JSON.parse(localStorage.getItem("celcius", celcius)) === false) {
    celcius = false;
  } else {
    celcius = true;
  }

  const setPosition = position => {
    let lat = position.coords.latitude;
    let lon = position.coords.longitude;
    axios
      .get(
        //Using proxy server hosted on heroku in order to hide public facing appid
        `https://proxy-server-for-homepage.herokuapp.com/api/?lat=${lat}&lon=${lon}`
      )
      .then(data => {
        loading = false;
        //VARIABLE FOR DATA FROM API
        incomeData = data.data;

        //TEMPERATURE
        temp = Math.round(incomeData.main.temp) - 273;

        //DESCRIPTION OF WEATHER
        desc = incomeData.weather[0].description;

        //USER'S CITY LOCATION
        location = incomeData.name;

        //GET ICON FOR WEATHER
        switch (incomeData.weather[0].icon) {
          //sunny
          case "01d":
            icon = "fas fa-sun";
            break;
          //cloudy
          case "02d":
            icon = "fas fa-cloud-sun";
            break;
          //scattered clouds
          case "03d":
            icon = "fas fa-cloud";
            break;
          //broken clouds
          case "04d":
            icon = "fas fa-cloud-meatball";
            break;
          //shower rain
          case "09d":
            icon = "fas fa-cloud-showers-heavy";
            break;
          //rain
          case "10d":
            icon = "fas fa-umbrella";
            break;
          //thunderstorm
          case "11d":
            icon = "fas fa-bolt";
            break;
          //snow
          case "13d":
            icon = "far fa-snowflake";
            break;
          //mist
          case "50d":
            icon = "fas fa-smog";
            break;
        }
      })
      .catch(err => {
        console.log(err.response);
        window.alert(err.response.data.message);
      });
  };

  if ("geolocation" in navigator) {
    navigator.geolocation.getCurrentPosition(setPosition);
  }
</script>

<style>
  h2 {
    cursor: pointer;
  }

  i {
    margin: 5px;
    font-size: 2em;
  }
</style>

{#if loading}
  <i class="fas fa-hourglass-half" />
{:else}

  <i class={icon} />

  <h1>{desc}</h1>

  <h2
    on:click={() => {
      celcius = !celcius;
      let str = JSON.stringify(celcius);
      localStorage.setItem('celcius', str);
    }}>
    {celcius ? `${temp}  ` : Math.round((temp * 9) / 5 + 32)} &deg {celcius ? 'C' : 'F'}
  </h2>

  <h3>{location}</h3>
{/if}
