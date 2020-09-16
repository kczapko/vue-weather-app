<template>
  <section class="search">
    <button class="search__close" @click="$emit('close-search')">
      <span class="search__close__icon material-icons">close</span>
    </button>
    <div class="search__bar">
      <div class="search__bar__wrapper">
        <span class="search__bar__wrapper__icon material-icons">search</span>
        <input
          class="search__bar__wrapper__input"
          type="text"
          placeholder="search location"
          v-model="location"
          @keyup.enter="searchCity"
        />
      </div>
      <button class="search__bar__button_submit" @click="searchCity">
        Search
      </button>
    </div>
    <div class="search__cities" v-if="cities.length">
      <ul class="search__cities__list">
        <li
          class="search__cities__list__city"
          v-for="city in cities"
          :key="city.woeid"
          @click="$emit('change-city', city.woeid)"
        >
          <span class="search__cities__list__city__name">{{ city.title }}</span>
          <span class="search__cities__list__city__icon material-icons"
            >chevron_right</span
          >
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  props: ["cities"],
  data() {
    return {
      location: "",
    };
  },
  methods: {
    searchCity() {
      this.$emit("search-city", this.location);
    },
  },
};
</script>

<style lang="scss">
.search {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  z-index: 2;
  background: #1e213a;
  padding: 82px 46px 42px;
  transition: transform 0.5s;
  transform: translateX(-100%);

  &--active {
    transform: translateX(0);
  }

  &__close {
    position: absolute;
    right: 46px;
    top: 20px;
    background: none;
    border: none;
    color: #e7e7eb;
    padding: 0;
    cursor: pointer;
    transition: transform 0.1s;

    &__icon {
      font-size: 20px;
    }

    &:hover {
      transform: scale(1.2);
    }
  }

  &__bar {
    margin-bottom: 58px;
    height: 48px;
    display: flex;
    justify-content: space-between;

    &__wrapper {
      position: relative;
      width: 100%;

      &__icon {
        position: absolute;
        left: 15px;
        top: 16px;
        font-size: 18px;
        color: #616475;
      }

      &__input {
        height: 100%;
        width: calc(100% - 20px);
        background: none;
        border: 1px solid #e7e7eb;
        padding-left: 51px;
        color: #e7e7eb;
      }
    }

    &__button_submit {
      border: 0;
      background: #3c47e9;
      color: #e7e7eb;
      padding: 0 20px;
      cursor: pointer;
      font-family: "Raleway", sans-serif;

      &:hover {
        background: darken(#3c47e9, 10);
      }
    }
  }

  &__cities {
    height: calc(100% - 58px - 48px);
    overflow: auto;

    &__list {
      list-style: none;
      margin: 0;
      padding: 0;

      &__city {
        height: 64px;
        line-height: 64px;
        position: relative;
        padding: 0 30px 0 12px;
        border: 1px solid transparent;
        position: relative;
        cursor: pointer;

        &__icon {
          color: #616475;
          font-size: 12px;
          position: absolute;
          right: 16px;
          top: 26px;
          opacity: 0;
        }

        &:hover {
          border: 1px solid #616475;

          .search__cities__list__city__icon {
            opacity: 1;
          }
        }
      }
    }
  }
}

@media (max-width: 1390px) {
  .search {
    padding: 62px 20px 42px;
    height: auto;

    &__close {
      right: 20px;
    }

    &__cities {
      height: auto;
      overflow: hidden;
    }
  }
}
</style>
