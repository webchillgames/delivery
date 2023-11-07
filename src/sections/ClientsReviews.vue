<template>
  <div class="wrapper clients-reviews">
    <h2>About us</h2>
    <div class="clients-reviews__arrows">
      <AppButton class="clients-reviews__arrow">
        <svg
          width="30"
          height="13"
          viewBox="0 0 30 13"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M23.8885 12.355L29.5 6.17749L28.5 5.07664V5.0039H28.4339L23.8885 0L22.4086 1.3464L25.731 5.0039L0 5.0039L0 7.0039L26.0464 7.0039L22.4086 11.0086L23.8885 12.355Z"
          />
        </svg>
      </AppButton>

      <AppButton class="clients-reviews__arrow">
        <svg
          width="30"
          height="13"
          viewBox="0 0 30 13"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M23.8885 12.355L29.5 6.17749L28.5 5.07664V5.0039H28.4339L23.8885 0L22.4086 1.3464L25.731 5.0039L0 5.0039L0 7.0039L26.0464 7.0039L22.4086 11.0086L23.8885 12.355Z"
          />
        </svg>
      </AppButton>
    </div>
    <p class="clients-reviews__subtitle">
      Out Awesome <br />
      Clients
    </p>

    <ul>
      <li v-for="r in reviews" :key="r.id">
        <div>
          <p>{{ r.text }}</p>
          <div>
            <img :src="r.avatar" />
            <span>{{ r.name }}</span>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import AppButton from "../elements/AppButton.vue";

const reviews = [
  {
    id: 1,
    avatar: "src/assets/review-1.jpg",
    name: `Isak Pettersson`,
    text: `Yes, you will need to have the land owner sign the permit application as the Permittee, and you sign the permit as the Applicant or Agent for the Permittee.`,
  },
  {
    id: 2,
    avatar: "src/assets/review-2.jpg",
    name: `Simon Sandberg`,
    text: `From most barricade or traffic control companies located in the phone book. They employ certified Traffic Control Supervisors (TCS) who can generate and certify the traffic control plan.`,
  },
  {
    id: 3,
    avatar: "src/assets/review-1.jpg",
    name: `Stan Smith`,
    text: `An A-Line, or access restriction deed is a property right that has been obtained by CDOT for the sole purpose of prohibiting direct`,
  },
];

export default {
  setup() {
    return { reviews };
  },
  components: { AppButton },
};
</script>

<style lang="scss">
.clients-reviews {
  display: grid;
  grid-template-columns: repeat(2, 1fr);

  h2 {
    @include sectionTitle;
  }

  ul {
    @include resetListStyles;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 20px;

    li {
      background-color: #fff;
      box-shadow: 0px 20px 40px 0px rgba(238, 77, 71, 0.1);
      border-radius: 10px;
      height: 360px;
      width: 420px;
      display: flex;
      justify-content: center;
      align-items: center;

      padding: 60px 50px;
      box-sizing: border-box;
      
      p {
        font-size: 16px;
        font-weight: 300;
        line-height: 30px;
        margin-bottom: 60px;
      }
    }
  }

  &__subtitle {
    @include sectionSubtitle;
  }

  &__arrow {
    @include iconButton;
    width: 90px;
    height: 90px;
    fill: $main;

    &:first-child {
      transform: rotate(180deg);
    }
  }

  &__arrows {
    display: flex;
  }
}
</style>
