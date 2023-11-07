<template>
  <div class="main">
    <h1 class="visually-hidden">TRAFICO</h1>
    <PageHeader />

    <main>
      <AboutUs class="main__section" />
      <HowTo class="main__section" />
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
import HowTo from "./sections/HowTo.vue";
import PageHeader from "./sections/PageHeader.vue";

export default {
  setup() {
    return {};
  },
  components: { PageHeader, AboutUs, HowTo, FAQ, ClientsReviews },
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
}
</style>
