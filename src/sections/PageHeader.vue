<template>
  <header class="page-header">
    <div class="wrapper page-header__wrapper">
      <div class="page-header__top">
        <img
          src="@/assets/logo.svg"
          width="215"
          height="50"
          alt="логотип"
          class="page-header__logo"
        />
        <img
          src="@/assets/logo-mobile.svg"
          width="47"
          height="50"
          alt="логотип"
          class="page-header__logo-mobile"
        />
        <nav>
          <div class="page-header__menu" :class="{ opened: isMenuOpened }">
            <ul>
              <li v-for="l in menuLinks" :key="l.id">
                <a href="/">{{ l.title }}</a>
              </li>
            </ul>

            <button
              @click="isMenuOpened = false"
              type="button"
              class="page-header__closer"
            >
              <img src="src/assets/cross.svg" />
            </button>
          </div>

          <AppButton title="contact us" class="page-header__button" />

          <AppButton
            @click="isMenuOpened = !isMenuOpened"
            title="menu"
            class="page-header__menu-button"
          />
        </nav>
      </div>

      <div class="page-header__content">
        <p>
          Your awesome <br />
          traffic permit <br />
          consultant.
        </p>
        <AppButton icon="arrow" title="get started" class="page-header__button" />
      </div>
    </div>

    <img src="src/assets/car.png" class="page-header__car" />
  </header>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import AppButton from "../elements/AppButton.vue";

const menuLinks = [
  { id: 1, title: "ABOUT", link: "" },
  { id: 2, title: "HOW TO", link: "" },
  { id: 3, title: "FAQS", link: "" },
];

export default defineComponent({
  setup() {
    const isMenuOpened = ref(false);

    return { menuLinks, isMenuOpened };
  },
  components: { AppButton },
});
</script>

<style lang="scss">
.page-header {
  height: 951px;
  background-image: url("src/assets/scene.png");
  background-size: contain;
  background-repeat: no-repeat;
  position: relative;
  margin-bottom: 15%;

  &__button,
  &__menu-button {
    @include coloredButton;
  }

  &__closer {
    @include iconButton;
  }

  &__car {
    position: absolute;
    left: 0;
    bottom: 0;
    transform: translate(-30%, 40%);
    height: 35%;
  }

  &__closer,
  &__logo-mobile,
  &__menu-button {
    display: none;
  }

  &__wrapper.wrapper {
    padding-top: 64px;
    padding-left: 240px;
    padding-right: 240px;
  }

  &__content {
    p {
      font-weight: 400;
      font-size: 100px;
      color: #fff;
      padding: 0;
      margin-bottom: 60px;
      font-family: "Times New Roman", Times, serif;
    }
  }

  nav {
    display: flex;
    align-items: center;
    position: relative;
  }

  ul {
    list-style: none;
    display: grid;
    grid-template-columns: repeat(3, max-content);
    margin: 0;
    padding: 0;

    a {
      color: #fff;
      font-weight: 700;
      text-decoration: none;
      cursor: pointer;
      transition: all 0.2s;
      padding: 20px 25px;
      border-radius: 8px;
      white-space: nowrap;
      display: flex;
      align-items: center;
      justify-content: center;

      &:hover {
        background-color: $main;
      }
    }
  }

  &__top {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  @media (max-width: $desktop) {
    &__content {
      p {
        font-size: 70px;
      }
    }

    &__wrapper {
      padding-top: 40px;
      padding-left: 200px;
      padding-right: 200px;
    }
  }

  @media (max-width: $middle-desktop) {
    height: 714px;

    &__car {
      height: 30%;
    }

    &__content {
      p {
        font-size: 50px;
      }
    }

    &__wrapper {
      padding-top: 30px;
      padding-left: 140px;
      padding-right: 140px;
    }

    &__logo {
      width: 150px;
    }
  }

  @media (max-width: $tablet) {
    height: 535px;

    &__car {
      height: 25%;
    }

    &__content {
      p {
        font-size: 40px;
      }
    }

    &__wrapper {
      padding-left: 100px;
      padding-right: 100px;
    }
  }

  @media (max-width: $small-tablet) {
    margin-bottom: 50px;
    height: auto;
    padding-bottom: 30px;
    background-image: none;
    background: linear-gradient(#f47f6b, #fbc2aa);

    &__car {
      display: none;
    }

    &__content {
      p {
        font-size: 30px;
      }
    }

    &__wrapper.wrapper {
      padding-left: 16px;
      padding-right: 16px;
    }

    &__closer {
      width: 20px;
      height: 20px;
      border: none;
      background-color: transparent;
      position: absolute;
      top: 12px;
      right: 20px;
      display: block;
    }

    &__menu-button {
      margin-left: 10px;
      display: flex;
    }

    &__menu {
      display: none;
      position: absolute;
      right: 0;
      top: 120%;
      background-color: rgba(#fff, 0.7);
      padding: 16px;
      border-radius: 8px;
      padding-right: 32px;
      padding-top: 32px;

      &.opened {
        display: block;
        animation-name: menuAnimatiom;
        animation-duration: 1s;
      }
    }

    ul {
      display: block;

      a {
        color: $main;
        padding: 10px;
      }
    }
  }

  @media (max-width: $phone) {
    &__logo-mobile {
      display: block;
    }

    &__logo {
      display: none;
    }
  }
}

@keyframes menuAnimatiom {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}
</style>
