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
      <v-card
        class="mx-auto rounded-lg"
      >
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title class="headline">
              {{ weather.name }}, {{ weather.sys.country }}
            </v-list-item-title>
            <v-list-item-subtitle>{{ dateBuilder() }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>

        <v-card-text>
          <v-row align="center">
            <v-col
              class="display-3 font-weight-bold black--text"
              cols="6"
            >
              {{ Math.round(weather.main.temp) }}&deg;C
            </v-col>
            <v-col cols="6">
              {{ weather.weather[0].main }}
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="6">
              <v-card
                color="#F5FAFF"
                width="150px"
              >
                <v-card-text>
                  <span class="font-weight-black text-h6">
                    Pressure
                  </span>
                  <br>
                  <span class="font-weight-bold text-subtitle-1">
                    {{ weather.main.pressure }} hpa
                  </span>
                </v-card-text>
              </v-card>
            </v-col>
            <v-col cols="6">
              <v-card
                color="#F5FAFF"
                width="150px"
              >
                <v-card-text>
                  <span class="font-weight-black text-h6">
                    Humidity
                  </span>
                  <br>
                  <span class="font-weight-bold text-subtitle-1">
                    {{ weather.main.humidity }} %
                  </span>
                </v-card-text>
              </v-card>
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
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
      console.log(this.weather);
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
