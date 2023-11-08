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

      <ul class="faq__list" ref="listRef" @click="changeOpenedItem"></ul>
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
    answer: `Traffic permits are a requirement for conducting professional traffic. Traffic permits are a requirement for conducting professional traffic. Traffic permits are a requirement for conducting professional traffic`,
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

const ITEM_HEIGHT = 90;
const ITEM_MARGIN = 45;

export default {
  setup() {
    const listRef = ref();

    function changeOpenedItem(e) {
      // const list = e.target.closest("ul");
      const item = e.target.closest("li");
      const answer = item.children.item(1);

      if (!item) return;

      const prevOpenedItem = document.querySelector("li.open");

      if (prevOpenedItem) {
        prevOpenedItem.classList.remove("open");
      }

      item.classList.add("open");

      placeListOnPage(answer.clientHeight, item.getAttribute("id"));
    }

    function createFaqList() {
      if (!listRef.value) {
        return;
      }

      list.forEach((el, i) => {
        const liEl = document.createElement("li");

        const questionEl = document.createElement("h3");
        const answerEl = document.createElement("p");

        const insideQuestion = document.createElement("span");
        const insideAnswer = document.createElement("span");

        liEl.setAttribute("id", i);

        insideQuestion.textContent = el.question;
        insideAnswer.textContent = el.answer;

        questionEl.style.height = ITEM_HEIGHT + "px";

        liEl.style.width = "40%";

        answerEl.appendChild(insideAnswer);
        questionEl.appendChild(insideQuestion);

        liEl.appendChild(questionEl);
        liEl.appendChild(answerEl);
        listRef.value.appendChild(liEl);
      });
    }

    function placeListOnPage(answerHeight, openedItemId) {
      const items = listRef.value.children;

      const halfOfItems = Math.ceil(items.length / 2);

      listRef.value.style.height =
        halfOfItems * ITEM_HEIGHT + ITEM_MARGIN * (halfOfItems - 1) + "px";

      if (answerHeight) {
        listRef.value.style.height =
          (halfOfItems - 1) * ITEM_HEIGHT +
          ITEM_MARGIN * (halfOfItems - 1) +
          answerHeight +
          ITEM_HEIGHT +
          "px";
      }

      for (let item of items) {
        const i = item.id;

        if (i < halfOfItems) {
          item.style.left = 0;
          item.style.top = ITEM_HEIGHT * i + "px";

          if (i > 0) {
            item.style.top = ITEM_HEIGHT * i + ITEM_MARGIN * i + "px";

            //openedItemId < i: открытый находится над текущим
            if (openedItemId && openedItemId < i) {
              item.style.top =
                ITEM_HEIGHT * i + answerHeight + ITEM_MARGIN * i + "px";
            }
          }
        } else {
          const itemIdxOfSecondColumn = i - halfOfItems;
          item.style.left = "50%";

          item.style.top = ITEM_HEIGHT * itemIdxOfSecondColumn + "px";

          if (itemIdxOfSecondColumn > 0) {
            item.style.top =
              ITEM_HEIGHT * itemIdxOfSecondColumn +
              ITEM_MARGIN * itemIdxOfSecondColumn +
              "px";

            if (openedItemId && openedItemId < i) {
              item.style.top =
                ITEM_HEIGHT * itemIdxOfSecondColumn + answerHeight;
              ITEM_MARGIN * itemIdxOfSecondColumn + "px";
            }
          }
        }
      }
    }

    onMounted(() => {
      createFaqList();
      placeListOnPage();
    });

    return { listRef, changeOpenedItem };
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
      margin: 0;
      position: absolute;
      transform: translateY(-100%);
      opacity: 0;
      box-shadow: 0px 20px 40px 0px rgba(238, 77, 71, 0.1);
    }

    li.open p {
      transform: translateY(0);
      opacity: 1;
    }

    button {
      @include iconButton;
    }
  }
}
</style>
