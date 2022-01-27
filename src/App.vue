<script setup>

</script>

<template>
  <article
    id="app"
    :class="
      typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : 'cold'
    "
  >
    <main>
      <SearchBar :onSearch='onSearch'/>
      <WeatherBox :weather="weather"/>
      
    </main>
  </article>
</template>

<script>

import SearchBar from './components/SearchBar.vue' 
import WeatherBox from './components/WeatherBox.vue'

export default {
  name: "app",
  components: {
    SearchBar,
    WeatherBox
  },

  data() {
    return {
      api_key: "d3b24a9953815f47c37c5c74a1927a76",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {

    onSearch(data) {
      this.query = data.query;
      this.fetchWeather()
    },

    fetchWeather() {
      console.log(this.query)
      fetch(
        `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
      )
        .then((res) => {
          return res.json();
        })
        .then(this.setResponse);
    },


    setResponse(res) {
      this.weather = res;
    },   
  },
};
</script>

<style>
@import "./assests/styles/main-styles.css";
@import "./assests/styles/weather-styles.css";

#app.cold {
  background-image: url("./assests/cold-bg.jpg");
}

#app.warm {
  background-image: url("./assests/warm-bg.jpeg");
}
</style>
