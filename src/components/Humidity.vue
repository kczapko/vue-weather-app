<template>
  <section class="humidity">
    <header class="humidity__title">Humidity</header>
    <div class="humidity__amount">
      <span class="humidity__amount__number">{{ humidity }}</span>
      <span class="humidity__amount__units">%</span>
    </div>
    <div class="humidity__progress">
      <div class="humidity__progress__numbers">
        <span>0</span>
        <span>50</span>
        <span>100</span>
      </div>
      <div class="humidity__progress__progressbar">
        <div
          class="humidity__progress__progressbar__bar"
          :style="{ width: `${humidity}%` }"
        ></div>
      </div>
      <div class="humidity__progress__units">%</div>
    </div>
  </section>
</template>

<script>
export default {
  props: ["humidity"],
};
</script>

<style lang="scss">
.humidity {
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

  &__progress {
    &__numbers {
      display: flex;
      justify-content: space-between;
      font-size: 12px;
    }

    &__units {
      font-size: 12px;
      text-align: right;
    }

    &__progressbar {
      margin: 2px 0;
      height: 8px;
      border-radius: 4px;
      background: #e7e7eb;
      position: relative;
      overflow: hidden;

      &__bar {
        position: absolute;
        left: 0;
        top: 0;
        height: 100%;
        background: #ffec65;
      }
    }
  }
}
</style>
