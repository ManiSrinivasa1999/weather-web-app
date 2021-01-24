<template>
  <div class="home">
    <div class="search-box">
      <v-text-field
        v-model="search"
        label="Search..."
        solo
        @keypress="fetchWeather"
        class="search-bar rounded-lg"
        append-icon="fas fa-search"
        prepend-inner-icon="fas fa-map-marker-alt"
      ></v-text-field>
    </div>
    <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
      <div class="location-box">
        <div class="location">
          {{ weather.name }}, {{ weather.sys.country }}
        </div>
        <div class="date">{{ dateBuilder() }}</div>
      </div>

      <div class="weather-box">
        <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
        <div class="weather">{{ weather.weather[0].main }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  components: {},
  data() {
    return {
      urlBase: 'https://api.openweathermap.org/data/2.5/',
      apiKey: '3e7c22fddbf2e104d77b9e54040865d0',
      search: '',
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key === 'Enter') {
        fetch(
          `${this.urlBase}weather?q=${this.search}&units=metric&APPID=${this.apiKey}`,
        )
          .then((res) => res.json())
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.search = '';
      this.weather = results;
    },
    dateBuilder() {
      const d = new Date();
      const months = [
        'January',
        'February',
        'March',
        'April',
        'May',
        'June',
        'July',
        'August',
        'September',
        'October',
        'November',
        'December',
      ];
      const days = [
        'Sunday',
        'Monday',
        'Tuesday',
        'Wednesday',
        'Thursday',
        'Friday',
        'Saturday',
      ];
      const day = days[d.getDay()];
      const date = d.getDate();
      const month = months[d.getMonth()];
      const year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    },
  },
};
</script>
