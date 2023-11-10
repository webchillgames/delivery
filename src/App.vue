<template>
  <div class="main">
    <h1 class="visually-hidden">TRAFICO</h1>
    <PageHeader />

    <main>
      <AboutUs class="main__section" />
      <HowToApply class="main__section" />
      <FAQ class="main__section" />
      <ClientsReviews class="main__section" />
    </main>
    <footer></footer>
  </div>
</template>

<script>
import AboutUs from "./sections/AboutUs.vue";
import ClientsReviews from "./sections/ClientsReviews.vue";
import FAQ from "./sections/FAQ.vue";
import HowToApply from "./sections/HowToApply.vue";
import PageHeader from "./sections/PageHeader.vue";

export default {
  setup() {
    return {};
  },
  components: { PageHeader, AboutUs, FAQ, ClientsReviews, HowToApply },
};
</script>

<style lang="scss">
@import "@/styles/base.scss";

.main {
  &__section {
    & + & {
      margin-top: 100px;
    }
  }

  @media (max-width: $small-tablet) {
    &__section {
      & + & {
        margin-top: 40px;
      }
    }
  }
}
</style>
