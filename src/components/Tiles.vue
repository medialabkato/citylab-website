<template>
  <section class="tiles">
    <div v-parallax.absY="parallax" class="horizontal-padding">
      <div class="row tiles__white">
        <div
          v-for="(tile, index) in data" 
          :key="index"
          class="columns small-12 medium-6 large-4 tiles__container" 
          :class="[
            {'tiles__container--single' : tile.links.length === 1 },
            {'tiles__container--double' : tile.links.length === 2 },
            {'tiles__container--four' : tile.links.length === 5 },
            `medium-order-${tile.medium_order} large-order-${tile.large_order}`
          ]"
        >
          <div class="tiles__tile" :class="[{'tiles__tile--double' : tile.links.length === 2 }, {'tiles__tile--four' : tile.links.length === 5 }]" v-for="link in tile.links" :key="link.href">
            <div class="tiles__cont">
              <a class="tiles__link" :href="link.href" target="_blank">
                <p v-html="link.title" class="tiles__title grafit orphan-check"></p>
                <p v-if="tile.links.length === 1" class="grafit">
                  <svg xmlns="http://www.w3.org/2000/svg" width="12.18" height="14" viewBox="0 0 12.18 14">
                    <path id="Path_191" data-name="Path 191" d="M5.264,11.692v8.2L3,17.684.9,19.756,7,25.692,13.076,19.7l-2.1-2.016-2.24,2.24V11.692Z" transform="translate(-0.896 -11.692)" fill="#2a2a2a"/>
                  </svg>
                </p>
                <p v-if="link.description" class="grafit tiles__description orphan-check">{{ link.description }}</p>
                <div class="tiles__right">
                  <img v-if="link.symbol" class="tiles__symbol" :src="`/svg/symbols/${link.symbol}.svg`" alt="">
                </div>
              </a>
              <div class="tiles__line"></div>
            </div>
            <div v-if="link.hover" class="tiles__hover" :style="`background-image: url(/hovers/${link.hover}.jpg)`"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import ScrollMonitor from 'scrollmonitor'

export default {
  name: 'Tiles',
  props: ['data'],
  data() {
    return {
      scrollMonitor: null
    }
  },
  mounted() {
    this.scrollMonitor = ScrollMonitor;
    const tiles = document.querySelectorAll(".tiles__tile");

    tiles.forEach(element => {
      const elementWatcher = scrollMonitor.create( element, -300 );
      
      elementWatcher.enterViewport(() => {
        if (window.matchMedia("(max-width: 640px)").matches) {
          element.classList.add('tiles__tile--active');
        }
      });
      elementWatcher.exitViewport(() => {
        if (window.matchMedia("(max-width: 640px)").matches) {
          element.classList.remove('tiles__tile--active');
        }
      });
    });
  },
  computed: {
    parallax() {
      if (window.matchMedia("(min-width: 1024px)").matches) {
        return -0.25
      } else {
        return 0
      }
    }
  }
}
</script>

<style lang="scss">
.tiles {
  background: white;
  transition: 0.3s;

  @include tablet {
    background: $purple;
  }

  &__container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;

    @include tablet {
      position: relative;
    }

    .tiles__tile--double:last-of-type { //biała kafelka koło zielonej na tablecie
      display: none;

      @include tablet {
        display: block;
        background: white;
        width: calc(50% - 0.625rem);
        transform: translateY(0);
        min-height: unset;
        height: unset;
        position: absolute;
        bottom: -55px;
        right: 0.3125rem;
        padding-bottom: calc(50% - 1 * 0.625rem);

        &:before, &:after {
          display: none;
        }
      }

      @include desktop {
        right: 0.3125rem;
        transition: 0.8s;
        bottom: -55px;

        &:hover {
          background: $highlight-green;
          div {
            p {
              color: $purple;
            }
          }
        }
      }
    }
    .tiles__tile--four:first-of-type {
      @include tablet {
        display: none;
      }
    }

    &--double {
      transform: translate(0);
    }

    &--double, &--four {
      position: relative;
      &:before {
        content: '';
        background: $purple; 
        width: calc(100% - 2 * 0.625rem);
        height: calc(100% + 32px);
        position: absolute;
        top: -42px;
        left: 0.625rem;

        @include tablet {
          display: none;
        }
      }
    }

    &--four {
      &:before {
        top: -10px;
        height: calc(100% + 12px);
      }
    }
  }

  &__cont {
    height: calc(100% - 20px);
  }

  &__link {
    @include tablet {
      position: absolute;
      display: block;
      top: 10px;
      left: 10px;
      width: calc(100% - 20px);
      height: 100%;
    }
  }

  &__tile {
    background: white;
    width: 100%;
    min-height: 215px;
    position: relative;
    margin-bottom: 10px;

    @include tablet {
      padding: 0 20px;
      min-height: unset;
      padding-bottom: 100%;
      margin-top: 0.3125rem;
      margin-bottom: 0.3125rem;
      
      p {
        margin: 10px 0;
      }
    }

    @include desktop {
      &:hover {
        .tiles__hover {
          visibility: visible;
          opacity: 1;
          pointer-events: none;
        }
      }
    }

    div {
      a {
        display: block;
        height: inherit;
      }
    }

    &--double { //zielona kafelka
      background: $highlight-green;
      height: 166px;
      transform: translateX(-20%);
      padding-left: 20%;
      margin-bottom: 60px;

      @include tablet {
        padding-left: 10px;
        padding-bottom: 130px;
        min-height: 80px;
        z-index: 4;
        transform: initial;
        padding-bottom: calc(50% - 0.3125rem);
      }

      @include desktop {
        min-height: unset;
        height: 60px;
      }

      &:hover {
        div {
          a {
            p {
              color: $purple;
            }
          }
        }
      }

      &:before {
        content: '';
        position: absolute;
        height: 50px;
        width: 35%;
        bottom: 0;
        left: 32%;
        z-index: 0;
        background: $highlight-green;
        transform: translateY(100%);

        @include tablet {
          position: fixed;
          top: .3125rem;
          width: calc(50% - 30px - .625rem);
          left: calc(30px + .3125rem);
          height: calc(100% - .625rem);
          transform: initial;
        }
      }

      &:after {
        content: '';
        position: absolute;
        height: 120px;
        width: 100vw;
        bottom: 0;
        right: 1px;
        background: $highlight-green;
        transform: translateX(100%);

        @include tablet {
          bottom: initial;
          top: 0;
          right: 0;
          width: 60px;
          height: 60px;
          transform: translateX(0);
          background: $purple;
        }
      }

      .tiles__line {
        display: none;
      }
    }

    &--four {
      width: calc(50% - 0.625rem);
      background: white;
      padding: 10px;
      min-height: calc(50% - (0.625rem ));
      margin-bottom: calc(2 * 0.625rem);
      box-sizing: border-box;

      .tiles__title, .tiles__description {
        margin-top: 0;
        margin-bottom: 0;
      }

      @include tablet {
        min-height: unset;
        padding-bottom: calc(45%);
        width: calc(50% - 0.3125rem);
        margin-bottom: 0.3125rem;
      }

      @include desktop {
        transition: 0.6s;

        &:hover {
          background: $highlight-green;
          div {
            p {
              color: $purple;
            }
          }
        }
      }
      
      .tiles__line {
        display: none;
      }
    }

    &--active {
      .tiles__hover {
        opacity: 1;
        visibility: visible;
        width: 100vw;
        transform: translate(-0.625rem, - 10px);
        height: 95%;

        @include tablet {
          opacity: 0;
          visibility: hidden;
          width: 100%;
          height: 100%;
          transform: initial;
        }
      }

      &.tiles__tile--four {
        background: $highlight-green;

        .tiles__link {
          p {
            color: $purple;

            @include tablet {
              color: black;
            }
          }
        }

        .tiles__hover {
          width: 100%;
          height: 100%;
          transform: initial;
        }

        @include tablet {
          background: white;

        }
      }
    }
  }
  
  &__line {
    background: $purple;
    height: 9px;
    width: 100%;

    @include tablet {
      display: none;
    }
  }

  &__description {
    width: 80%;

    @include tablet {
      width: 100%;
    }
  }

  &__right {
    width: 100%;
    text-align: right;

    @include tablet {
      position: absolute;
      bottom: 20px;
      right: 20px;
    }
  }

  &__symbol {
    padding-bottom: 32px;
    margin-left: auto;
  }

  &__white {
    position: relative;

    @include tablet {
      .columns {
        padding-right: 0.3125rem;
        padding-left: 0.3125rem;
      }
    }

    &:before {
      content: '';
      background: white;
      width: 100%;
      height: 80%;
      position: absolute;
      top: 20%;
      left: 0;
      transform: translateX(calc(-100% + 1.40625rem + 1px));
      z-index: 3;
      display: none;

      @include tablet {
        display: none;
      }

      @include desktop {
        display: block;
        transform: translateX(calc(-100% + 0.3125rem + 1px));
        height: calc(100% + 45px);
        top: -50px;
      }

      @include large-desktop {
        height: calc(100% + 95px);
        top: -100px;
      }
    }
  }

  &__hover {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-size: cover; 
    background-position: center;
    visibility: hidden;
    opacity: 0;
    transition: 0.3s ease-out;
    z-index: 3;
  }
}
</style>