<template>
  <section class="hero horizontal-padding">
    <div class="row">
      <div class="columns small-12 medium-2 hero__flex">
        <a class="hide-tablet" href="https://medialabkatowice.eu" target="_blank">
          <img src="/svg/logos/medialab.svg" alt="Logo Medialab">
        </a>
        <a class="hide-tablet" href="/">
          <img src="/svg/logos/citylab.svg" alt="Logo City Lab">
        </a>
        <a class="hide-until-tablet" href="https://medialabkatowice.eu" target="_blank">
          <img class="hero__both" src="/svg/logos/both.svg" alt="Logo Medialab i City Lab">
        </a>
      </div>
      <div class="columns medium-8 medium-offset-2 hero__container">
        <h1 class="hero__title hide-until-tablet" v-html="data.header"></h1>
      </div>
    </div>
    <div class="row">
      <div class="columns small-12">
        <div class="hero__line"></div>
      </div>
      <div class="columns small-12 medium-8 medium-offset-4">
        <div class="hero__content">
          <h1 v-parallax="-0.3" class="hero__title hide-tablet" v-html="data.header"></h1>
          <div v-parallax="-0.1" v-html="joinSliderContent" class="orphan-check"></div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Hero',
  props: ['data'],
  data() {
    return {
      active: 0
    }
  },
  computed: {
    joinSliderContent() {
      return this.data.slider.join(' ')
    }
  }
}
</script>

<style lang="scss">
.hero {
  background: $purple;
  padding-top: 15px;

  @include tablet {
    padding-top: 0;
  }

  &__title {
    font-size: rem(24px);
    margin-bottom: 0;
    text-transform: uppercase;
    
    @include tablet {
      margin-bottom: 10px;
    }

    @include desktop {
      font-size: rem(26px);
      margin-bottom: 15px;
    }

    span {
      display: block;

      @include tablet {
        display: inline;
      }
    }
  }

  &__container {
    display: none;

    @include tablet {
      display: flex;
      align-items: flex-end;
    }
  }

  &__line {
    width: 100%;
    height: 1px;
    background: white;
    position: relative;
    z-index: 3;
    display: none;

    @include tablet {
      display: block;
    }
  }

  &__content {
    padding-top: 90px;
    padding-bottom: 125px;

    @include tablet {
      padding-top: 25px;
    }

    @include desktop {
      padding-top: 30px;
      margin-top: 0;
      padding-bottom: 15px;
    }
  }

  &__flex {
    display: flex;
    justify-content: space-between;
    
    @include tablet {
      position: relative;
      &:before {
        content: '';
        width: 1px;
        height: 100%;
        background: white;
        position: absolute;
        top: 0; 
        right: 0;
      }
    }
  }

  &__both {
    width: 60px;

    @include tablet {
      padding: 15px 0;
    }

    @include desktop {
      width: 150px;
      padding: 50px 0;
    }
  }

  .glide {
    div[data-glide-el="controls"] {
      display: flex;
      justify-content: flex-end;
      transform: translateY(-100px);
      
      button {
        letter-spacing: 2.5px;
        font-size: 13px;

        &:first-of-type {
          transform: scaleX(-1) translateX(27px);
        }

        &:last-of-type {
          transform: translateX(10px);
        }
      }
    }
  }
}
</style>