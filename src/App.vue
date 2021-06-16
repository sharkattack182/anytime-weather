<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Search..." v-model="query" @keypress="fetchWeather" />
      </div>
      {{ query}}
      <div class="weather-wrap" v-if="typeof weather.main !== 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
          <div class="date">Tuesday June 16 2021</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{ Math.round((weather.main.temp - 273.15) * 9 / 5 + 32) }} </div>
          <div class="weather">{{ weather.weather[0].main}}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "23346a4286e014dc1c7ba261140705ca",
      url_base: "http://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {}
    };
  },
  methods: {
    fetchWeather(e) {
      if(e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&appid=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
      }
    },
    setResults(results) {
      console.log(this.weather)
      this.weather = results;
      console.log(this.weather)
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
} 

body {
  font-family: "montserrat", sans-serif;
}

#app {
  background-image: url("./assets/warm.png");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75));
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s
}


.search-box .search-bar:focus{ 
   box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
   background-color: rgba(255, 255, 255, 0.75);
   border-radius: 16px 0px 16px 0px;
}

.location-box .location {
  color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgb(0, 0, 0, 0.25);
}

.location-box .date {
  color: #FFF;
  font-size: 20px;
  font-weight: 300;
  text-align: center;
  font-style: italic;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #FFF;
  font-size: 102px;
  font-weight: 900;
  
  text-shadow: 3px 6px rgb(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0;

  box-shadow: 3px 6px rgb(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: #FFF;
  font-weight: 700;
  font-size: 48px;
  text-shadow: 3px 6px rgb(0, 0, 0, 0.25);
  font-style: italic;
}

</style>
