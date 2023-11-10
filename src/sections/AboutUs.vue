<template>
  <div class="wrapper about-us">
    <div class="about-us__text">
      <h2>About us</h2>
      <p>
        The occupational traffic permit is one of the most important things in
        the company when carrying out freight transport. In fact, it is a
        prerequisite for doing business traffic at all.
      </p>

      <div class="about-us__question">
        <p>
          How do you do when you need to obtain a commercial traffic permit for
          freight transport to your business?
        </p>
      </div>
    </div>
    <img src="src/assets/about.png" width="500" />
  </div>
</template>

<script>
export default {
  setup() {
    return {};
  },
};
</script>

<style lang="scss">
.about-us {
  @include paragraphBlock;

  p {
    @include paragraph;
  }

  h2 {
    @include sectionTitle;
  }

  &__question {
    background-color: rgba($main, 0.1);
    border-left: 10px solid $main;
    padding: 30px 45px;

    p {
      font-size: 24px;
      font-weight: 500;
      line-height: 36px;
      padding: 0;
      margin: 0;
    }
  }

  img {
    @include paragraphImg;
  }

  @media (max-width: $small-tablet) {


    &__text {
      grid-row: 2 / -1;
    }
  }
}
</style>
