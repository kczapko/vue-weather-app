<template>
  <section class="pressure">
    <header class="pressure__title">Air Pressure</header>
    <div class="pressure__amount">
      <span class="pressure__amount__number">{{ Math.round(pressure) }}</span>
      <span class="pressure__amount__units">mb</span>
    </div>
  </section>
</template>

<script>
export default {
  props: ["pressure"],
};
</script>

<style lang="scss">
.pressure {
  background: #1e213a;
  padding: 22px 40px;

  &__title {
    text-align: center;
    margin-bottom: 10px;
  }

  &__amount {
    text-align: center;
    margin-bottom: 12px;

    &__number {
      font-size: 64px;
      font-weight: 700;
    }

    &__units {
      font-size: 24px;
    }
  }
}
</style>
