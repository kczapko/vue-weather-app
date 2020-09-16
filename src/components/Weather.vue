<template>
  <section class="weather">
    <div class="weather__top">
      <button class="weather__top__button_search" @click="$emit('open-search')">
        Search for places
      </button>
      <button class="weather__top__button_location">
        <span
          class="weather__top__button_location__icon material-icons"
          @click="$emit('geolocation-search')"
          >gps_fixed</span
        >
      </button>
    </div>
    <div class="weather__image">
      <img class="weather__image__image" :src="image" alt="" />
    </div>
    <div class="weather__temperature">
      <span class="weather__temperature__number">{{ temperature }}</span>
      <span class="weather__temperature__degree">°{{ temperatureUnit }}</span>
    </div>
    <div class="weather__name">{{ weather.weather_state_name }}</div>
    <div class="weather__date">
      <span class="weather__date__today">Today</span>
      <span class="weather__date__spacer">•</span>
      <span class="weather__date__day">{{ date }}</span>
    </div>
    <div class="weather__location">
      <span class="weather__location__icon material-icons">place</span>
      <span class="Weather__location__city">{{ city }}</span>
    </div>
  </section>
</template>

<script>
export default {
  props: ["weather", "city", "farenheit"],
  computed: {
    temperature() {
      if (this.farenheit) {
        return `${Math.round(this.weather.the_temp * 1.8 + 32)}`;
      } else {
        return `${Math.round(this.weather.the_temp)}`;
      }
    },
    temperatureUnit() {
      if (this.farenheit) {
        return "F";
      } else {
        return "C";
      }
    },
    date() {
      return this.$moment(this.weather.applicable_date).format("ddd, D MMM");
    },
    image() {
      let url = "";
      switch (this.weather.weather_state_name) {
        case "Snow":
          url = require("../assets/img/Snow.png");
          break;
        case "Sleet":
          url = require("../assets/img/Sleet.png");
          break;
        case "Hail":
          url = require("../assets/img/Hail.png");
          break;
        case "Thunderstorm":
          url = require("../assets/img/Thunderstorm.png");
          break;
        case "Heavy Rain":
          url = require("../assets/img/HeavyRain.png");
          break;
        case "Light Rain":
          url = require("../assets/img/LightRain.png");
          break;
        case "Showers":
          url = require("../assets/img/Shower.png");
          break;
        case "Heavy Cloud":
          url = require("../assets/img/HeavyCloud.png");
          break;
        case "Light Cloud":
          url = require("../assets/img/LightCloud.png");
          break;
        case "Clear":
          url = require("../assets/img/Clear.png");
          break;
      }

      return url;
    },
  },
};
</script>

<style lang="scss">
.weather {
  width: 100%;
  height: 100%;
  background: #1e213a;
  position: relative;
  padding: 42px 46px 32px;

  &:before {
    content: "";
    pointer-events: none;
    position: absolute;
    left: 0;
    top: 0;
    display: block;
    height: 100%;
    width: 100%;
    background: url("../assets/img/Cloud-background.png") no-repeat 50% 50px;
    opacity: 0.1;
  }

  &__top {
    display: flex;
    justify-content: space-between;
    margin-bottom: 110px;

    &__button_search {
      cursor: pointer;
      border: 0;
      padding: 0 18px;
      color: #e7e7eb;
      text-align: center;
      height: 40px;
      font-size: 16px;
      font-family: "Raleway", sans-serif;
      line-height: 19px;
      background: #6e707a;
      box-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);

      &:hover {
        background: darken(#6e707a, 10);
      }
    }

    &__button_location {
      cursor: pointer;
      border: 0;
      color: #e7e7eb;
      text-align: center;
      height: 40px;
      width: 40px;
      line-height: 14px;
      border-radius: 50%;
      background: #6e707a;
      box-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);

      &:hover {
        background: darken(#6e707a, 10);
      }

      &__icon {
        font-size: 22px;
      }
    }
  }

  &__image {
    height: 300px;
    text-align: center;
  }

  &__temperature {
    text-align: center;
    margin-bottom: 80px;

    &__number {
      font-size: 144px;
    }

    &__degree {
      color: #a09fb1;
      font-size: 40px;
    }
  }

  &__name {
    text-align: center;
    font-weight: 600;
    font-size: 36px;
    color: #a09fb1;
    margin-bottom: 80px;
  }

  &__date {
    text-align: center;
    color: #88869d;
    font-size: 18px;
    margin-bottom: 20px;

    &__spacer {
      margin: 0 15px;
    }
  }

  &__location {
    text-align: center;
    color: #88869d;
    font-size: 18px;

    &__icon {
      font-size: 20px;
      margin-right: 5px;
      vertical-align: middle;
    }
  }
}

@media (max-width: 1390px) {
  .weather {
    height: auto;
    padding: 42px 20px 32px;
  }
}
</style>
