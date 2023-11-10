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
import { computed, onMounted, onUnmounted, ref } from "vue";
import QAItem from "../elements/QAItem.vue";

const list = [
  {
    id: 0,
    question: `What is a professional traffic permit? What is a professional traffic permit?`,
    answer: `Traffic permits are a requirement for conducting professional traffic. Traffic permits are a requirement for conducting professional traffic. Traffic permits are a requirement for conducting professional traffic`,
  },
  {
    id: 1,
    question: `How to check the traffic condition?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 2,
    question: `What are the requirements for a professional traffic permit?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 3,
    question: `Are there professional traffic permit training courses at a distance?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 4,
    question: `When is a professional traffic permit needed?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 5,
    question: `Where to look for a traffic permit?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 6,
    question: `Are there differences between a traffic permit and a professional traffic permit?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 7,
    question: `How to plug in for the traffic permit test?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
  {
    id: 8,
    question: `How is the sample for a professional traffic permit booked?`,
    answer: `Traffic permits are a requirement for conducting professional traffic.`,
  },
];

const ITEM_WIDTH = 48;
const ITEM_MARGIN = 45;

export default {
  setup() {
    const maxHeight = ref(0);

    const itemHeight = computed(() => maxHeight.value + 30);
    const listRef = ref();

    function changeOpenedItem(e) {
      const item = e.target.closest("li");
      const answer = item.children.item(1);

      if (!item) return;

      const prevOpenedItem = document.querySelector("li.open");

      if (prevOpenedItem) {
        prevOpenedItem.classList.remove("open");
      }

      item.classList.add("open");

      placeListOnPage(answer.clientHeight, Number(item.getAttribute("id")));
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

      for (let item of items) {
        const itemId = Number(item.id);
        let currentIdx;
        item.style.width = ITEM_WIDTH + "%";

        if (itemId < halfOfItems) {
          item.style.left = 0;
          currentIdx = itemId;
        } else {
          item.style.left = "52%";
          currentIdx = itemId - halfOfItems;
        }

        const title = item.children.item(0);
        const text = item.children.item(0).children.item(0);

        if (maxHeight.value < text.getBoundingClientRect().height) {
          maxHeight.value = text.getBoundingClientRect().height;
        }

        title.style.height = itemHeight.value + "px";

        item.style.top = itemHeight.value * currentIdx + "px";

        if (currentIdx > 0) {
          item.style.top =
            itemHeight.value * currentIdx + ITEM_MARGIN * currentIdx + "px";
        }

        if (openedItemId !== undefined && itemId > openedItemId) {
          const isItemFrom1Column = itemId < halfOfItems;
          const isItemFrom2Column = itemId >= halfOfItems;

          const isOpenedItemFrom1Column = openedItemId < halfOfItems;
          const isOpenedItemFrom2Column = openedItemId >= halfOfItems;

          if (isOpenedItemFrom1Column && isItemFrom1Column) {
            item.style.top =
              itemHeight.value * itemId +
              answerHeight +
              ITEM_MARGIN * itemId +
              "px";
          }

          if (isOpenedItemFrom2Column && isItemFrom2Column) {
            item.style.top =
              itemHeight.value * currentIdx +
              answerHeight +
              ITEM_MARGIN * currentIdx +
              "px";
          }
        }
      }

      if (maxHeight.value > 0) {
        listRef.value.style.height =
          halfOfItems * itemHeight.value +
          ITEM_MARGIN * (halfOfItems - 1) +
          "px";

        if (answerHeight) {
          listRef.value.style.height =
            (halfOfItems - 1) * itemHeight.value +
            ITEM_MARGIN * (halfOfItems - 1) +
            answerHeight +
            itemHeight.value +
            "px";
        }
      }
    }

    onMounted(() => {
      createFaqList();
      placeListOnPage();

      window.addEventListener("resize", placeListOnPage);
    });

    onUnmounted(() => {
      window.removeEventListener("resize", placeListOnPage);
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
    border-top-left-radius: 80px;
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
      padding: 8px;
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

  @media (max-width: $desktop) {
  }

  @media (max-width: $middle-desktop) {
    img {
      width: 500px;
    }
  }

  @media (max-width: $tablet) {
    ul {
      h3 {
        font-size: 16px;
      }
    }

    img {
      width: 400px;
    }
  }

  @media (max-width: $small-tablet) {
    padding-top: 40px;

    &::after {
      border-top-left-radius: 40px;
    }

    &__top {
      display: block;
      text-align: center;
    }

    img {
      display: none;
    }
  }
}
</style>
