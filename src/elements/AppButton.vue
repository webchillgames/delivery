<template>
  <button type="button" class="app-button">
    <span v-if="title"> {{ title }} </span>
    <img v-if="icon" :src="`src/assets/${icon}.svg`" />
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: {
    icon: {
      type: String,
      required: false,
    },
    title: {
      type: String,
      required: false,
    },
  },

  setup() {
    return {};
  },
};
</script>
