<template>
  <div id="app">
    <div class="mobile-menu" v-if="isMenuOpen">
      <div class="mobile-menu__background" @click="toggleMobileMenu"></div>
      <div class="mobile-menu__list-wrapper">
        <div class="mobile-menu__close">
          <span class="mobile-menu__close-icon" @click="toggleMobileMenu"></span>
        </div>
        <ul class="mobile-menu__list">
          <li v-for="item in menu" :key="item.id" class="mobile-menu__item">
            <a :href="item.href" class="mobile-menu__link h3" :class="'mobile-menu__link_' + menu.id">{{ item.text }}</a>
          </li>
        </ul>
      </div>
    </div>
    <section class="section section_top">
      <div class="container">
        <header class="header">
          <div class="header__item header__item_logo">
            <Logo />
          </div>
          <div class="header__item header__item_menu">
            <Menu :menu="menu" />
          </div>
          <div class="header__item header__item_search">
            <Search />
          </div>
          <div class="header__item header__item_menu-mobile">
            <span @click="toggleMobileMenu" class="header__button-mobile" :class="(isMenuOpen) ? 'header__button-mobile_open' : ''"></span>
          </div>
        </header>
      </div>
    </section>
    <section class="section section_content">
      <div class="container">
        <div class="paintings">
          <h1>
            {{ heading }}
          </h1>
          <ul class="paintings__list">
            <li class="paintings__item" v-for="item in paintings" :key="item.id">
              <Painting :id="item.id" :image="item.image" :title="item.title" :price="item.price" :old-price="item.oldPrice" :for-sale="item.forSale"/>
            </li>
          </ul>
        </div>
      </div>
    </section>
    <section class="section section_bottom">
      <div class="container">
        <footer class="footer">
          <div class="footer__item footer__item_logo">
            <Logo />
          </div>
          <div class="footer__item footer__item_menu">
            <Menu :menu="menu" :place="'footer'"/>
          </div>
          <div class="footer__item footer__item_contacts">
            <Contacts />
          </div>
        </footer>
      </div>
    </section>
  </div>
</template>

<script>

import Menu from './components/Menu.vue';
import Logo from './components/Logo.vue';
import Search from './components/Search.vue';
import Painting from './components/Painting.vue';
import Contacts from './components/Contacts.vue';

export default {
  name: 'App',
  components: {
    Menu,
    Logo,
    Search,
    Painting,
    Contacts
  },
  data () {
    return {
      heading: 'Картины эпохи Возрождения',
      isMenuOpen: false,
      menu: [
        {
          id: 1,
          href: '#',
          text: 'Каталог'
        },
        {
          id: 2,
          href: '#',
          text: 'Доставка'
        },
        {
          id: 3,
          href: '#',
          text: 'Оплата'
        },
        {
          id: 4,
          href: '#',
          text: 'Контакты'
        },
        {
          id: 5,
          href: '#',
          text: 'О галерее'
        },
      ],
      paintings: [
        {
          id: 0,
          image: require('@/assets/images/paintings/item1.jpg'),
          title: '«Рождение Венеры» Сандро Боттичелли',
          price: '1 000 000 $',
          oldPrice: '2 000 000 $',
          forSale: true
        },
        {
          id: 1,
          image: require('@/assets/images/paintings/item2.jpg'),
          title: '«Тайная вечеря» Леонардо да Винчи',
          price: '3 000 000 $',
          forSale: true
        },
        {
          id: 2,
          image: require('@/assets/images/paintings/item3.jpg'),
          title: '«Сотворение Адама» Микеланджело',
          price: '5 000 000 $',
          oldPrice: '6 000 000 $',
          forSale: true
        },
        {
          id: 3,
          image: require('@/assets/images/paintings/item4.jpg'),
          title: '«Урок анатомии» Рембрандт',
          forSale: false
        },
      ]
    }
  },
  methods: {
    toggleMobileMenu () {
      if (this.isMenuOpen) {
        this.isMenuOpen = false
      } else {
        this.isMenuOpen = true
      }
    }
  }
}
</script>

<style lang="scss">
@import '@/assets/styles/normalize.css';

@mixin mobile-button {
  display: block;
  background-color: #403432;
  position: absolute;
  height: 4px;
  width: 30px;
  transition: transform 400ms cubic-bezier(0.23, 1, 0.32, 1);
  border-radius: 2px;
}

@font-face {
    font-family: 'Merriweather';
    src: local('Merriweather Bold'), local('Merriweather-Bold'),
        url('@/assets/fonts/Merriweather-Bold.woff2') format('woff2'),
        url('@/assets/fonts/Merriweather-Bold.woff') format('woff');
    font-weight: bold;
    font-style: normal;
    font-display: swap;
}
@font-face {
    font-family: 'Merriweather';
    src: local('Merriweather Regular'), local('Merriweather-Regular'),
        url('@/assets/fonts/Merriweather-Regular.woff2') format('woff2'),
        url('@/assets/fonts/Merriweather-Regular.woff') format('woff');
    font-weight: normal;
    font-style: normal;
    font-display: swap;
}
@font-face {
    font-family: 'Merriweather';
    src: local('Merriweather Light'), local('Merriweather-Light'),
        url('@/assets/fonts/Merriweather-Light.woff2') format('woff2'),
        url('@/assets/fonts/Merriweather-Light.woff') format('woff');
    font-weight: 300;
    font-style: normal;
    font-display: swap;
}
h1,
.h1 {
  font-size: 24px;
  font-weight: 700;
  line-height: 36px;
  margin-bottom: 39px;
  margin-top: 0;
}
h2,
.h2 {
  font-size: 18px;
  line-height: 27px;
}
h3,
.h3 {
  font-size: 16px;
  font-weight: 700;
  line-height: 24px
}
h4,
.h4 {
  font-size: 14px;
  font-weight: 700;
  line-height: 21px;
}
h5,
.h5 {
  font-size: 14px;
  font-weight: 400;
  line-height: 21px;
}
h6,
.h6 {
  font-size: 14px;
  font-weight: 300;
  line-height: 21px;
}
* {
  font-family: Merriweather, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #343030;
  box-sizing: border-box;
}
.button {
  display: inline-block;
  padding: 14px 28px;
  background: #403432;
  color: #F4F6F9;
  font-size: 14px;
  line-height: 21px;
  border: 0;
  cursor: pointer;

  &__text {
    color: #F4F6F9;
  }

  &:hover {
    background: #776763;
  }

  &:disabled {
    pointer-events: none;
    background: #C1B4B1;
  }
}

.container {
  display: block;
  max-width: 1216px;
  width: 100%;
}

.section {
  display: flex;
  justify-content: center;
  overflow: hidden;

  &_top {
    border-bottom: 1px solid #E1E1E1 ;
  }

  &_content {
    padding: 45px 0 25px;
  }

  &_bottom {
    background: #ECEAEA;
  }
}

.paintings {
  &__list {
    padding-left: 0;
    list-style: none;
    display: flex;
    flex-wrap: wrap;
    align-items: flex-start;
    margin: 0 -16px;
  }

  &__item {
    width: 100%;
    max-width: 25%;
    padding: 0 16px; 
    margin-bottom: 20px;
  }
}

.header,
.footer {
  display: flex;
  align-items: center;
  padding: 24px 0;
  &__item {
    &_logo {
      margin-right: 48px;
    }

    &_search,
    &_contacts {
      margin-left: auto;
    }
  }
}

.mobile-menu {
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  z-index: 20;
  display: flex;
  justify-content: flex-end;

  &__background {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background: rgba(64, 52, 50, 0.5);
  }

  &__close {
    position: absolute;
    top: 28px;
    right: 50px;
    &-icon {
      background: rgba(255, 255, 255, 0);

      &::before {
        @include mobile-button;
        content: "";
        margin-top: 0px;
        transform: rotate(405deg);
      }

      &::after {
        @include mobile-button;
        content: "";
        margin-top: 0px;
        transform: rotate(-405deg);
      }
    }
  }

  &__list {
    padding-left: 0;
    padding-top: 12px;
    margin-top: 0;
    margin-bottom: 0;
    list-style: none;
    display: flex;
    flex-direction: column;

    &-wrapper {
      position: relative;
      z-index: 20;
      width: 400px;
      background: #FFFFFF;
    }
  }

  &__item {
    display: block;
    width: 100%;
    padding: 12px 24px;
  }

  &__link {
    text-decoration: none;
  }
}

@media all and (max-width: 1259px) {
  .container {
    max-width: 991px;
  }

  .paintings {
    &__item {
      max-width: 33.3333%;
    }
  }
}

@media all and (min-width: 1045px) {
  .mobile-menu {
    display: none !important;
  }

  .header {
    &__item {
      &_menu-mobile {
        display: none !important;
      }
    }
  }
}

@media all and (max-width: 1044px) {
  .container {
    max-width: 720px;
  }

  .header {
    &__item {
      &_menu {
        display: none;
      }

      &_menu-mobile {
        width: 30px;
        margin-left: 20px;
      }
    }

    &__button-mobile {
      @include mobile-button;

      &::before {
        @include mobile-button;
        content: "";
        margin-top: -8px;
      }

      &::after {
        @include mobile-button;
        content: "";
        margin-top: 8px;
      }

      &_open {
        opacity: 0.5;
      }
    }
  }

  .paintings {
    &__item {
      max-width: 50%;
    }
  }

  .footer {
    flex-wrap: wrap;
    &__item {
      &_contacts {
        margin-left: 0;
        display: flex;
        justify-content: flex-end;
        width: 100%;
      }
    }
  }
}

@media all and (max-width: 769px) {
  .container {
    max-width: 100%;
    padding: 0 20px;
  }

  .mobile-menu {
    &__list-wrapper {
      width: 100%;
    }
  }
}

@media all and (max-width: 599px) {
  .paintings {
    &__item {
      max-width: 100%;
    }
  }

  .footer {
    flex-direction: column;
    align-items: flex-start;

    &__item {
      &_contacts {
        margin-left: 0;
      }
    }
  }
}


</style>
