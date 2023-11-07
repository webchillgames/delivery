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

      <ul class="faq__list" ref="listRef">
        <!-- <QAItem
          v-for="q in faqList"
          :key="q"
          :item="q"
          :isOpened="openedItem === q.id"
          @changeOpenedItem="changeOpenedItem"
        /> -->
        <!-- <li class="faq__load">Load more</li> -->
      </ul>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";
import QAItem from "../elements/QAItem.vue";

const list = [
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

const ITEM_HEIGHT = 90

export default {
  setup() {
    const openedItem = ref(null);
    const listRef = ref();

    function changeOpenedItem(id) {
      console.log(id);
      if (openedItem.value === id) {
        openedItem.value = null;
      } else {
        openedItem.value = id;
      }
    }

    function createFaqList() {
      if (!listRef.value) {
        return;
      }
      const halfOfItems = Math.ceil(list.length / 2);

      listRef.value.style.height = halfOfItems * 90 + "px";

      list.forEach((el, i) => {
        const liEl = document.createElement("li");

        const questionEl = document.createElement("h3");
        const answerEl = document.createElement("p");

        const insideQuestion = document.createElement("span");
        const insideAnswer = document.createElement("span");

        insideQuestion.textContent = el.question;
        insideAnswer.textContent = el.answer;

        liEl.style.width = "40%";

        if (i < halfOfItems) {
          liEl.style.left = 0;
          liEl.style.top = 90 * i + "px";
        } else {
          console.log(Math.round(i - halfOfItems));
          liEl.style.top = 90 * (i - halfOfItems) + "px";
          liEl.style.left = "50%";
        }

        answerEl.appendChild(insideAnswer);
        questionEl.appendChild(insideQuestion);

        liEl.appendChild(questionEl);
        liEl.appendChild(answerEl);

        listRef.value.appendChild(liEl);
      });
    }

    onMounted(createFaqList);

    return { listRef, openedItem, changeOpenedItem };
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

  &__load {
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
    order: 1;
  }

  ul {
    border: 1px solid red;
    @include resetListStyles;
    position: relative;

    li {
      cursor: pointer;
      box-shadow: 0px 20px 40px 0px rgba(238, 77, 71, 0.1);
      align-self: flex-start;
      position: absolute;
    }

    h3,
    p {
      padding: 16px;
      box-sizing: border-box;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    h3 {
      height: 90px;
      font-size: 18px;
      font-weight: 500;
      line-height: 30px;
      background-color: #fff;
      border-radius: 10px;
      margin: 0;
    }

    p {
      border-bottom-left-radius: 10px;
      border-bottom-right-radius: 10px;
      position: relative;

      span {
        position: absolute;
        transform: translateY(-100%);
        // opacity: 0;
      }
    }

    button {
      @include iconButton;
    }
  }
}
</style>
