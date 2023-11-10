<template>
  <div class="how-to wrapper">
    <img src="src/assets/apply.png" width="500" />
    <div>
      <h2>How to apply</h2>
      <p>
        When applying for a traffic permit, there are certain requirements that
        you must meet that are included in the examination: requirements for
        professional knowledge, solid establishment, good reputation and
        financial resources. Important to remember is to confirm your
        application for a traffic permit by the company's company signer or CEO.
      </p>
    </div>
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
.how-to {
  @include paragraphBlock;

  p {
    @include paragraph;
  }

  h2 {
    @include sectionTitle;
  }

  img {
    @include paragraphImg;
  }
}
</style>
