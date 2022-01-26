<script setup>
</script>

<template>
  <article
    id="app"
    :class="
      typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''
    "
  >
    <main>
      <SearchBar :onSearch='onSearch'/>

      <section class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <section class="location-box">
          <section class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </section>
          <section class="date">{{ dateBuilder() }}</section>
        </section>

        <section class="weather-box">
          <section class="temp">{{ Math.round(weather.main.temp) }}°C</section>
          <section class="weather">{{ weather.weather[0].main }}</section>
        </section>
      </section>
    </main>
  </article>
</template>

<script>

import SearchBar from './components/SearchBar.vue' 


export default {
  name: "app",
  components: {
    SearchBar
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
    dateBuilder() {
      let d = new Date();
      const months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      const days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return ` ${day} ${date} ${month} ${year}`;
    },
  },
};
</script>

<style>
@import "./assests/styles/main-styles.css";
@import "./assests/styles/weather-styles.css";

#app {
  background-image: url("./assests/cold-bg.jpg");
}

#app.warm {
  background-image: url("./assests/warm-bg.jpeg");
}
</style>
