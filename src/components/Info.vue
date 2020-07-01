<template functional>
  <section class="info">
    <div class="horizontal-padding">
      <div class="row">
        <div v-parallax="-0.2" class="columns small-12 medium-6 large-7 purple info__text">
          <div class="purple info__header">INFO</div>
          <div v-html="props.data.info_text" class="orphan-check"></div>
        </div>
        <div  class="columns small-12 medium-6 large-5 purple info__contact">
          <div v-parallax="-0.1" v-html="props.data.contact" class="orphan-check"></div>
        </div>
      </div>
    </div>
  </section>
</template>
<style lang="scss">
.info {
  background: $highlight-green;

  @include tablet {
    background: white;
  }

  &__header {
    margin-top: 0px;
    margin-bottom: 35px;

    @include tablet {
      margin-top: 30px;
    }

    @include desktop {
      margin-bottom: 108px;
      margin-top: 50px;
    }
  }

  &__contact {
    margin-top: 0px;
    padding-bottom: 80px;
    position: relative;
    a {
      display: block;
    }

    &:before {
      content: '';
      width: 50vw;
      height: 50px;
      background: $highlight-green;
      position: absolute;
      bottom: 0;
      left: 50%;
      transform: translateY(100%);
    }

    @include tablet {
      background: $highlight-green;
      margin-top: 90px;
      
      p, a {
        position: relative;
        z-index: 999;
      }

      &:before {
        left: 0;
        bottom: initial;
        top: 0;
        height: calc(100% + 50px);
        width: 100vw;
        transform: translateY(0);
      }
    }

    @include desktop {
      p {
        margin-bottom: 80px;
        margin-top: 70px;
      }

      &:before {
        left: -250px;
        height: calc(100% + 220px);
      }
    }
  }

  &__text {
    @include tablet {
      background: $highlight-green;
      position: relative;
      padding-bottom: 60px;

      &:before {
        content: '';
        width: 50vw;
        height: 100%;
        background: $highlight-green;
        position: absolute;
        top: 0;
        left: 1px;
        transform: translateX(-100%);
      }
    }
    @include desktop {
      padding-bottom: 160px;
      z-index: 2;
    }
  }
}
</style>