<template functional>
  <section class="link-section">
    <div class="horizontal-padding">
      <div class="row">
        <div v-parallax="-0.06 * index" class="columns small-11 medium-6 large-4" v-for="(link, index) in props.data.links" :key="link.header">
          <a :href="link.link.href" class="link-section__link" target="_blank">
            <p class="link-section__text grafit orphan-check">{{ link.header }}</p>
            <p class="link-section__text purple orphan-check">{{ link.link.title }}</p>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss">
.link-section {
  background: white;
  padding-top: 140px;
  padding-bottom: 80px;

  @include tablet {
    position: relative;
    z-index: 2;
  }

  @include desktop {
    padding-top: 360px;
    padding-bottom: 216px;
    margin-top: -10px;
  }

  &__text {
    position: relative;
    z-index: 1;
    text-transform: uppercase;
  }

  &__link {
    position: relative;
    display: block;
    &:before {
      content: '';
      width: 0%;
      height: 115px;
      background: $highlight-green;
      position: absolute;
      top: 0;
      left: 0;
    }

    @include desktop {
      &:hover {
        &::before {
          animation: link-hover 0.8s ease-in-out forwards;
        }
      }
    }
  }

  @keyframes link-hover {
    0% {
      width: 0%;
    }

    100% {
      width: 100%;
    }
  }
}
</style>