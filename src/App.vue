<template>
  <div id="app">
    <loading v-if="loading === true"></loading>
    <div class="error" v-if="error" @click="error = ''">
      <span class="error__message">{{ error }}</span>
      <span class="error__close">x</span>
    </div>
    <div class="app__left" v-if="loading === false">
      <weather
        :weather="todayWeather"
        :city="city"
        :farenheit="isFarenheit"
        @open-search="searchActive = true"
        @geolocation-search="geolocation"
      ></weather>
      <search
        :class="{ 'search--active': searchActive }"
        :cities="cities"
        @close-search="searchActive = false"
        @change-city="
          woeid = $event;
          searchActive = false;
        "
        @search-city="searchCity($event)"
      ></search>
    </div>
    <div class="app__right" v-if="loading === false">
      <div class="temperature_switch">
        <button
          @click="isFarenheit = false"
          class="temperature_switch__button"
          :class="{
            'temperature_switch__button--active': !isFarenheit,
          }"
        >
          °C
        </button>
        <button
          @click="isFarenheit = true"
          class="temperature_switch__button"
          :class="{
            'temperature_switch__button--active': isFarenheit,
          }"
        >
          °F
        </button>
      </div>
      <five-day-weather
        :weather="nextDaysWeather"
        :farenheit="isFarenheit"
      ></five-day-weather>
      <section class="highlights">
        <header class="highlights__title">Today's Higlights</header>
        <div class="highlights__body">
          <wind
            :direction="todayWeather.wind_direction"
            :speed="todayWeather.wind_speed"
            :compass="todayWeather.wind_direction_compass"
          ></wind>
          <humidity :humidity="todayWeather.humidity"></humidity>
          <visibility :visibility="todayWeather.visibility"></visibility>
          <pressure :pressure="todayWeather.air_pressure"></pressure>
        </div>
      </section>

      <footer class="app__footer">Krzysztof Czapko @ DevChallenges.io</footer>
    </div>
  </div>
</template>

<script>
import axios from "axios";

import Weather from "./components/Weather.vue";
import Search from "./components/Search.vue";
import FiveDayWeather from "./components/FiveDayWeather.vue";
import Wind from "./components/Wind.vue";
import Humidity from "./components/Humidity.vue";
import Visibility from "./components/Visibility.vue";
import Pressure from "./components/Pressure.vue";
import Loading from "./components/Loading.vue";

export default {
  name: "App",
  data() {
    return {
      woeid: null,
      weather: [],
      cities: [],
      city: "",
      searchActive: false,
      isFarenheit: false,
      loading: true,
      error: "",
    };
  },
  watch: {
    woeid: function(val) {
      this.loading = true;
      this.getWeather();
    },
  },
  components: {
    Weather,
    Search,
    FiveDayWeather,
    Wind,
    Humidity,
    Visibility,
    Pressure,
    Loading,
  },
  mounted() {
    this.geolocation();
  },
  methods: {
    geolocation() {
      this.loading = true;
      navigator.geolocation.getCurrentPosition(
        (data) => {
          const { latitude, longitude } = data.coords;
          this.searchByLatLon(latitude, longitude);
        },
        (error) => {
          this.error = "Geolocation failed. Getting data for default city.";
          this.woeid = 523920; //Warsaw
          this.loading = false;
        }
      );
    },
    async searchByLatLon(lat, lon) {
      const { data } = await axios.get(
        `https://cors-anywhere.herokuapp.com/https://www.metaweather.com/api/location/search/?lattlong=${lat},${lon}`
      );

      if (data && data.length) {
        this.cities = data;
        this.woeid = data[0].woeid;
      } else {
        this.error =
          "Getting nearby cities failed. Getting data for default city.";
        this.woeid = 523920; //Warsaw
        this.loading = false;
      }
    },
    async getWeather() {
      const { data } = await axios.get(
        `https://cors-anywhere.herokuapp.com/https://meta-weather.now.sh/api/location/${this.woeid}/`
      );

      if (data) {
        this.weather = data.consolidated_weather;
        this.city = data.title;
      } else {
        this.error = "Getting weather data failed.";
      }

      this.loading = false;
    },
    async searchCity(name) {
      this.loading = true;
      const { data } = await axios.get(
        `https://cors-anywhere.herokuapp.com/https://www.metaweather.com/api/location/search/?query=${name}`
      );

      if (data && data.length) {
        this.woeid = data[0].woeid;
        this.searchActive = false;
      } else {
        this.error = "No data for given location";
        this.loading = false;
      }
    },
  },
  computed: {
    todayWeather() {
      return this.weather[0];
    },
    nextDaysWeather() {
      return this.weather.slice(1);
    },
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
  background: #100e1d;
  color: #e7e7eb;
  font-family: "Raleway", sans-serif;
  font-weight: 500;
  font-size: 16px;
}

*,
*::after,
*::before {
  box-sizing: border-box;
}

#app {
  width: 100%;
  min-height: 100vh;
  display: flex;

  .app__left {
    width: 460px;
    flex-shrink: 0;
    position: relative;
  }

  .app__right {
    flex: 1;
    padding: 42px 100px;
  }

  .app__footer {
    text-align: center;
    font-weight: 600;
    font-size: 14px;
    color: #616475;
  }
}

@media (max-width: 1390px) {
  #app {
    flex-wrap: wrap;

    .app__left {
      width: 100%;
    }

    .app__right {
      padding: 42px 20px;
    }
  }
}

.temperature_switch {
  display: flex;
  justify-content: flex-end;
  margin-bottom: 60px;

  &__button {
    height: 40px;
    width: 40px;
    border: 0;
    text-align: center;
    font-family: "Raleway", sans-serif;
    font-size: 18px;
    font-weight: 700;
    background: #585676;
    color: #e7e7eb;
    border-radius: 50px;
    margin-left: 12px;
    cursor: pointer;

    &--active {
      background: #e7e7eb;
      color: #110e3c;
    }
  }
}

@media (max-width: 1390px) {
  .temperature_switch {
    display: none;
  }
}

.highlights {
  margin-bottom: 50px;

  &__title {
    font-size: 24px;
    font-weight: 700;
    margin-bottom: 30px;
  }

  &__body {
    display: grid;
    grid-template-columns: repeat(2, minmax(280px, 1fr));
    grid-gap: 48px;
  }
}

@media (max-width: 1390px) {
  .highlights {
    &__body {
      grid-template-columns: repeat(1, minmax(280px, 1fr));
    }
  }
}

.error {
  position: fixed;
  z-index: 3;
  left: 50%;
  top: 20px;
  background: rgba(255, 0, 0, 0.3);
  border: 1px solid red;
  border-radius: 4px;
  color: #e7e7eb;
  padding: 10px 40px 10px 10px;
  transform: translateX(-50%);
  font-size: 14px;
  max-width: 80%;

  &__close {
    margin-left: 20px;
    font-size: 12px;
    display: inline-block;
    width: 18px;
    height: 18px;
    line-height: 17px;
    text-align: center;
    background: rgba(255, 0, 0, 0.6);
    border-radius: 50%;
    position: absolute;
    right: 10px;
    top: 8px;
  }
}
</style>
