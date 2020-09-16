<template>
  <section class="visibility">
    <header class="visibility__title">Visibility</header>
    <div class="visibility__amount">
      <span class="visibility__amount__number">{{
        visibility.toFixed(1)
      }}</span>
      <span class="visibility__amount__units">miles</span>
    </div>
  </section>
</template>

<script>
export default {
  props: ["visibility"],
};
</script>

<style lang="scss">
.visibility {
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
