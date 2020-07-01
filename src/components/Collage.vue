<template>
  <section class="collage">
    <div class="horizontal-padding">
      <div class="row">
        <div class="columns small-12">
          <div class="purple collage__header">
            MEDIALAB SPACES
            <img src="/svg/arrow-bottom.svg" alt="">
          </div>
        </div>
      </div>
      <div  class="row">
        <div class="columns small-12">
          <div class="collage__container">
            <img v-parallax="isDesktop ? 0.06 : null" src="/svg/purple-arrow.svg" class="collage__arrow" alt="">
            <div v-parallax="isDesktop ? -0.06 : null" @click="currentPhoto = currentPhoto === 1 ? 2 : 1" class="collage__photo" :class="currentPhoto === 2 ? 'collage__photo--second' : 'collage__photo--first'">
              <img src="/img/photo-1.jpg" alt="Zdjęcie Medialab Spaces">
            </div>
            <div v-parallax="isDesktop ? -0.1 : null" @click="currentPhoto = currentPhoto === 2 ? 1 : 2" class="collage__photo" :class="currentPhoto === 1 ? 'collage__photo--second' : 'collage__photo--first'">
              <img src="/img/photo-2.jpg" alt="Zdjęcie Medialab Spaces">
            </div>
            <div v-parallax="isDesktop ? -0.15 : null" class="collage__purple"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Collage',
  data() {
    return {
      currentPhoto: 1
    }
  },
  computed: {
    isDesktop() {
      return window.matchMedia("(min-width: 1024px)").matches
    }
  }
}
</script>

<style lang="scss">
.collage {
  background: white;
  padding-top: 103px;
  padding-bottom: 83px;

  @include desktop {
    padding-top: 220px;
    padding-bottom: 370px;
  }

  &__header {
    margin-bottom: 30px;

    @include tablet {
      margin-bottom: 55px;
    }
  }

  &__container {
    position: relative;
    height: 120vw;
    background: transparent;

    @include tablet {
      height: 75vw;
    }

    @include desktop {
      height: 40vw;
    }

    @include large-desktop {
      height: 37vw;
    }
  }

  &__arrow {
    width: 43px;
    position: absolute;
    top: 0;
    right: 0;
    z-index: 5;

    @include desktop {
      width: 63px;
    }
  }

  &__photo {
    transition: top 0.5s ease-in-out, left 0.5s ease-in-out, z-index 0.7s 0.2s ease-in-out;

    img {
      object-fit: cover;
    }

    @include desktop {
      cursor: pointer;

      img {
        transition: 0.6s ease-in-out;

        &:hover {
          transform: scale(0.99)
        }
      }
    }
  }

  &__photo--first {
    max-width: unset;
    width: 100vw;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 4;

    @include tablet {
      width: 80%;
      left: 10%;
    }
  }

  &__photo--second {
    max-width: unset;
    width: 110vw;
    position: absolute;
    top: 10%;
    right: -10vw;
    z-index: 3;

    @include tablet {
      width: 60%;
      top: 15%;
      right: initial;
      left: 0;
    }
  }

  &__purple {
    width: 100%;
    padding-bottom: 62%;
    background: $purple;
    position: absolute;
    bottom: 20%;
    right: 24%;
    z-index: 2;

    @include tablet {
      width: 75%;
      right: 0;
      bottom: initial;
      top: 20%;
      padding-bottom: 45%;
    }
  }
}
</style>