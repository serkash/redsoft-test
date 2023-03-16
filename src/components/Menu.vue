<template>
  <div class="nav" :class="'nav_' + place">
    <ul class="nav__list">
      <li v-for="item in menu" :key="item.id" class="nav__item">
        <a :href="item.href" class="nav__link" :class="'nav__link_' + menu.id">{{ item.text }}</a>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  name: 'MenuVue',
  props: {
    place: {
      type: String,
      default: 'header'
    },
    menu: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style scoped lang="scss">
  .nav {
    &__list {
      padding-left: 0;
      list-style: none;
      display: flex;
      align-items: center;
    }

    &__item {
      display: block;
      margin-right: 48px;

      &:last-child {
        margin-right: 0;
      }
    }

    &__link {
      text-decoration: none;
      font-size: 14px;
      line-height: 21px;
    }
  }

  @media all and (max-width: 1259px) {
    .nav {
      &__item {
        margin-right: 24px;
      }
    }
  }

  @media all and (max-width: 599px) {
    .nav {
      &__list {
        flex-direction: column;
        align-items: flex-start;
        margin-bottom: 0;
      }

      &__item {
        margin-right: 0;
        margin-bottom: 20px;

        &:last-child {
          margin-bottom: 10px;
        }
      }
    }
  }
</style>