<template>
  <div class="cookies" v-show="!closed">
    <div class="row align-items-center">
      <div class="columns small-9 large-10">
        <div v-html="data"></div>
      </div>
      <div class="columns small-3 large-2 text-right">
        <button @click="closeCookies" class="cookies__close" title="Zamknij informację nt. plików cookies.">OK!</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Cookies',
  props: ['data'],
  data() {
    return {
      more: false,
      closed: true,
    };
  },
  created() {
    if (localStorage.getItem('cookies') === null) {
      this.closed = false;
    }
  },
  methods: {
    closeCookies() {
      this.closed = true;
      localStorage.setItem('cookies', 'true');
    },
  },
};
</script>

<style lang="scss" scoped>
.cookies {
  position: fixed;
  bottom: 0;
  z-index: 99;
  left: 0;
  left: 0;
  background: $purple;
  padding: 10px 0;
  font-weight: 500;
  border: 1px solid $highlight-green;
  font-size: rem(18px);

  @include tablet {
    width: 70%;
    left: 30%;
  }

  @include desktop {
    font-size: rem(28px);
    width: 45%;
    left: 55%;
    padding: 38px;
    padding-right: 0;
  }

  &__close {
    background: $highlight-green;
    color: $purple;
    font-weight: 500;
    cursor: pointer;
    margin-right: 10px;

    @include desktop {
      margin-right: 45px;
    }
  }
}
</style>