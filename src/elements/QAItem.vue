<template>
  <li class="qa-item">
    <div class="qa-item__question" @click="$emit('changeOpenedItem', item.id)">
      <h3>{{ item.question }}</h3>
      <button type="button" :class="{ opened: isOpened, closed: !isOpened }">
        <Transition name="fade" mode="out-in">
          <img v-if="isOpened" src="src/assets/minus.svg" />
          <img v-else src="src/assets/plus.svg" />
        </Transition>
      </button>
    </div>
    <Transition name="answer">
      <div v-if="isOpened" class="qa-item__answer">
        <p>{{ item.answer }}</p>
      </div>
    </Transition>
  </li>
</template>

<script>
export default {
  emits: ["changeOpenedItem"],
  props: {
    item: {
      type: Object,
      required: true,
    },
    isOpened: {
      type: Boolean,
      required: true,
    },
  },

  setup() {},
};
</script>

<style lang="scss">
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.qa-item {
  cursor: pointer;
  box-shadow: 0px 20px 40px 0px rgba(238, 77, 71, 0.1);
  overflow: hidden;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
  align-self: flex-start;

  h3 {
    font-size: 18px;
    font-weight: 500;
    line-height: 30px;
  }

  button {
    @include iconButton;
  }

  &__question {
    border-radius: 10px;
    background-color: #fff;
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 90px;
    box-sizing: border-box;
  }

  &__question,
  &__answer {
    padding: 8px 16px;
  }
}
</style>
