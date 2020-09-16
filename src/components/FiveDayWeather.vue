<template>
  <section class="weather_5day">
    <div
      class="weather_5day__box"
      v-for="(day, index) in weather"
      :key="day.id"
    >
      <div class="weather_5day__box__date">
        {{ date(day.applicable_date, index) }}
      </div>
      <div class="weather_5day__box__image">
        <img
          class="weather_5day__box__image__image"
          :src="image(day.weather_state_name)"
          alt=""
        />
      </div>
      <div class="weather_5day__box__temperature">
        <span class="weather_5day__box__temperature__max">{{
          maxTemperature(day.max_temp)
        }}</span>
        <span class="weather_5day__box__temperature__min">{{
          minTemperature(day.min_temp)
        }}</span>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  props: ["weather", "farenheit"],
  methods: {
    date(date, index) {
      if (index == 0) {
        return "Tomorrow";
      } else {
        return this.$moment(date).format("ddd, D MMM");
      }
    },
    image(name) {
      let url = "";
      switch (name) {
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
    minTemperature(temp) {
      if (this.farenheit) {
        return `${Math.round(temp * 1.8 + 32)}°F`;
      } else {
        return `${Math.round(temp)}°C`;
      }
    },
    maxTemperature(temp) {
      if (this.farenheit) {
        return `${Math.round(temp * 1.8 + 32)}°F`;
      } else {
        return `${Math.round(temp)}°C`;
      }
    },
  },
};
</script>

<style lang="scss">
.weather_5day {
  display: grid;
  grid-template-columns: repeat(5, minmax(120px, 1fr));
  grid-gap: 26px;
  margin-bottom: 70px;

  &__box {
    background: #1e213a;
    padding: 18px 20px;

    &__date {
      text-align: center;
      margin-bottom: 15px;
    }

    &__image {
      margin-bottom: 25px;
      height: 62px;

      &__image {
        display: block;
        max-width: 100%;
        max-height: 100%;
        margin: auto;
      }
    }

    &__temperature {
      display: flex;
      justify-content: space-between;

      &__min {
        color: #a09fb1;
      }
    }
  }
}

@media (max-width: 1390px) {
  .weather_5day {
    grid-template-columns: repeat(2, minmax(120px, 1fr));

    &__box {
      &__image {
        height: 82px;
      }
    }
  }
}
</style>
