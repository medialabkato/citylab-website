<template >
  <footer class="footer">
    <div class="row expanded">
      <div class="columns large-2 footer__square"></div>
    </div>
    <div class="horizontal-padding">
      <div v-parallax="-0.03" class="row">
        <div class="columns small-10 small-offset-1 medium-offset-0 medium-2 medium-order-4 footer__languages">
          <a :class="{ 'footer__language--active' : language === 'pl'}" href="/">PL</a> | 
          <a :class="{ 'footer__language--active' : language === 'en'}" href="?lang=en">EN</a>
        </div>
        <div class="columns small-6 medium-3 medium-order-1 footer__logo">
          <a href="https://medialabkatowice.eu" target="_blank">
            <img src="/svg/logos/medialab-large.svg" alt="Logo Medialab">
          </a>
        </div>
        <div class="columns small-6 medium-3 medium-order-2 footer__logo">
          <a href="http://miasto-ogrodow.eu" target="_blank">
            <LogoKatowice />
          </a>
        </div>
        <div class="columns small-10 small-offset-1 medium-offset-0 medium-4 medium-order-3 footer__policy">
          <a :href="data.privacy_policy.href" target="_blank">
            {{ data.privacy_policy.title }}
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import LogoKatowice from './LogoKatowice'
export default {
  name: 'Footer',
  props: ['data', 'language'],
  components: {
    LogoKatowice
  }
}
</script>

<style lang="scss">
.footer {
  background: $purple;
  font-size: rem(18px);
  font-weight: 500;
  padding: 20px 0;

  @include desktop {
    padding: 30px 0 140px 0;
  }

  &__languages {
    text-align: center;
    padding-bottom: 20px;
    border-bottom: 1px solid white;
    margin-bottom: 40px;

    @include tablet {
      padding-bottom: 0;
      border-bottom: none;
      margin-bottom: 0;
      display: flex;
      align-items: center;
    }

    @include desktop {
      display: flex;
      justify-content: flex-end;
    }
  }

  &__language {
    &--active {
      font-weight: 700;
    }
  }

  &__policy {
    margin-top: 40px;
    border-top: 1px solid white;
    padding-top: 20px;
    text-align: center;

    @include tablet {
      margin-top: 0;
      padding-bottom: 20px;
      border-top: none;
      border-left: 1px solid white;
      border-right: 1px solid white;
      text-align: left;
    }

    @include desktop {
      padding: 55px 0;
      text-align: center;
    }
  }

  &__logo {
    text-align: center;
    img {
      width: 80%;
      margin: 0 auto;
    }

    @include tablet {
      display: flex;
      align-items: center;
    }
  }

  &__square {
    height: 100px;
    background: $purple;
    transform: translateY(-128px);
    display: none;

    @include desktop {
      display: flex;
    }
  }
}
</style>