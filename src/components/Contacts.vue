<template>
    <div class="contacts">
      <ul class="contacts__list">
        <li v-for="item in contacts" :key="item.id" class="contacts__item">
          <a :href="item.href" class="contacts__link" :class="'contacts__link_' + item.id">
            <img :src="item.icon" class="contacts__icon">
            <span class="contacts__value">
              {{ item.text }}
            </span>
          </a>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  
  export default {
    name: 'ContactsVue',
    props: {
      place: {
        type: String,
        default: 'header'
      }
    },
    data () {
      return {
        contacts: [
          {
            id: 1,
            href: 'tel:74955555555',
            text: '+7 (495) 555-55-55',
            icon: require('@/assets/icons/phone.svg')
          },
          {
            id: 2,
            href: 'https://yandex.ru/maps/213/moscow/house/ulitsa_raspletina_24/Z04Ycg9kS00HQFtvfXt4dXhmYw==/?ll=37.484280%2C55.794457&z=16.33',
            text: 'г. Москва, ул. Расплетина, 24',
            icon: require('@/assets/icons/place.svg')
          }
        ]
      }
    }
  }
  </script>
  
  <style scoped lang="scss">
  .contacts {

    &__list {
      padding-left: 0;
      list-style: none;
      display: flex;
      align-items: center;
    }

    &__item {
      margin-right: 48px;

      &:last-child {
        margin-right: 0;
      }
    }

    &__link {
      display: flex;
      align-items: center;
      text-decoration: none;
      font-size: 14px;
      line-height: 21px;
    }

    &__icon {
      margin-right: 8px;
    }
  }

  @media all and (max-width: 1259px) {
    .contacts {
      &__item {
        margin-right: 24px;
      }
    }
  }

  @media all and (max-width: 599px) {
    .contacts {
      &__list {
        flex-direction: column;
        align-items: flex-start;
      }

      &__item {
        margin-bottom: 20px;

        &:last-child {
          margin-bottom: 0;
        }
      }
    }
  }
  </style>