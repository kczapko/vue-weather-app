<template>
  <section class="wind">
    <header class="wind__title">Wind status</header>
    <div class="wind__speed">
      <span class="wind__speed__number">{{ Math.round(speed) }}</span>
      <span class="wind__speed__units">mph</span>
    </div>
    <div class="wind__direction">
      <span
        class="wind__direction__arrow"
        :style="{ transform: `rotate(${direction}deg)` }"
      >
        <span class="wind__direction__arrow__icon material-icons"
          >navigation</span
        >
      </span>
      <span class="wind__direction__name">{{ compass }}</span>
    </div>
  </section>
</template>

<script>
export default {
  props: ["direction", "speed", "compass"],
};
</script>

<style lang="scss">
.wind {
  background: #1e213a;
  padding: 22px 40px;

  &__title {
    text-align: center;
    margin-bottom: 10px;
  }

  &__speed {
    text-align: center;
    margin-bottom: 20px;

    &__number {
      font-size: 64px;
      font-weight: 700;
    }

    &__units {
      font-size: 24px;
    }
  }

  &__direction {
    text-align: center;

    &__arrow {
      display: inline-block;
      width: 30px;
      height: 30px;
      border-radius: 50px;
      text-align: center;
      background: rgba(255, 255, 255, 0.3);
      margin-right: 10px;
      line-height: 30px;

      &__icon {
        font-size: 14px;
      }
    }

    &__name {
      font-size: 14px;
    }
  }
}
</style>
