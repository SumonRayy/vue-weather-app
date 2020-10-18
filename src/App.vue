<template>
  <div id="app" :class="typeof weather.main != 'undefined' &&  weather.main.temp > 30 ? 'hot' : '' || typeof weather.main != 'undefined' &&  weather.main.temp > 16 ? 'warm' : ''"
    >
    <main>
      <div class="logo">
        abahawa <div class="name">by <a href="https://github.com/SumonRayy">sumonrayy</a></div>
      </div>
      <div class="search-box">
        <input type="text" 
        class="search-bar" 
        placeholder="Search Here. . . " 
        v-model="query"
        @keyup.enter="fetchWeather"
        />
        <button type="submit" v-on:click="fetchWeather" ><i class="fa fa-search"></i></button>
      </div>

      <div class="weather-wrap" v-if="typeof weather.main  != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{  weather.sys.country }}</div>
          <div class="date">{{ dateBuild() }}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      api_key: '', // 👈 Enter Your personal api key here
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods:{
    fetchWeather() {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
    },
    setResults(results)  {
          this.weather = results;
    },
    dateBuild () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: 'montserrat', sans-serif;
}

#app {
  background-image: url('https://i.imgur.com/K60tlp9.png');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

#app.warm {
  background-image: url('https://i.imgur.com/R4vOVS0.png');
}

#app.hot {
  background-image: url('https://i.imgur.com/SOm7X5g.png');
}

main{
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(to bottom,  rgba(0, 0, 0, 0.15), rgba(0, 0,  0, 0.75));

}

.logo {
  text-align: center;
  padding: 10px 25px;
  color: #fff;
  font-size: 50px;
  font-weight: 1000;
}

.logo .name {
  font-size: 14px;
  padding-bottom: 25px;
}

.search-box{
  margin-bottom: 30px;
  
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;
  border: none;
  outline: none;
  background: none;

  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}

.search-box button {
  margin: auto;
  margin-top: 5px;

  display: block;
  width: 10%;
  padding: 10px;

  color: #ffffffcb;
  font-size: 20px;
  border: none;
  outline: none;
  background: none;

  background-color: none;
  border-radius: 6px 6px 6px 6px;
  transition: 0.4s;
  cursor: pointer;
}

.search-box button:hover {
  background-color: rgba(255, 255, 255, 0.5);
  color: #313131;
}

.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 100px;
  font-weight: 1000;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: #fff;
  font-size: 50px;
  font-family: Arial, Helvetica, sans-serif;
  font-style: italic;
  font-weight: 700;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}


</style>



