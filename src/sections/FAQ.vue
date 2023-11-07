<template>
  <div class="faq">
    <div class="wrapper">
      <div class="faq__top">
        <div>
          <h2>FAQ</h2>
          <p class="faq__subtitle">
            Questions and Answers <br />
            on Professional Traffic <br />
            Permits:
          </p>
        </div>
        <img src="@/assets/faq.png" width="707" alt="вопросы" />
      </div>

      <ul>
        <QAItem
          v-for="q in faqList"
          :key="q"
          :item="q"
          :isOpened="openedItem === q.id"
          @changeOpenedItem="changeOpenedItem"
        />
        <li>Load more</li>
      </ul>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import QAItem from "../elements/QAItem.vue";

const faqList = [
  {
    id: 1,
    question: `What is a professional traffic permit?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 2,
    question: `How to check the traffic condition?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 3,
    question: `What are the requirements for a professional traffic permit?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 4,
    question: `Are there professional traffic permit training courses at a distance?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 5,
    question: `When is a professional traffic permit needed?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 6,
    question: `Where to look for a traffic permit?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 7,
    question: `Are there differences between a traffic permit and a professional traffic permit?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 8,
    question: `How to plug in for the traffic permit test?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 9,
    question: `How is the sample for a professional traffic permit booked?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
];

export default {
  setup() {
    const openedItem = ref(null);

    function changeOpenedItem(id) {
      console.log(id);
      if (openedItem.value === id) {
        openedItem.value = null;
      } else {
        openedItem.value = id;
      }
    }

    return { faqList, openedItem, changeOpenedItem };
  },
  components: { QAItem },
};
</script>

<style lang="scss">
.faq {
  padding-top: 120px;
  padding-bottom: 120px;
  position: relative;

  &::after {
    position: absolute;
    content: "";
    background-color: rgba($main, 0.1);
    width: 80%;
    height: 100%;
    top: 0;
    right: 0;
    z-index: -1;
    border-top-left-radius: 10%;
  }

  h2 {
    @include sectionTitle;
  }

  &__top {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 30px;
    margin-bottom: 90px;
  }

  &__subtitle {
    @include sectionSubtitle;
  }

  ul {
    @include resetListStyles;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 30px;

    li {
      &:last-child {
        background-color: rgba($main, 0.1);
        color: $main;
        font-size: 18px;
        font-weight: 700;
        line-height: 30px;
        letter-spacing: 0.9px;
        padding: 8px 16px;
        box-sizing: border-box;
        border-radius: 10px;
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;

        height: 90px;
      }
    }
  }
}
</style>
