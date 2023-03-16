<template>
  <div href="/" class="search">
    <form action="#" class="search__form">
      <input type="search" class="search__input" :placeholder="placeholder">
      <button type="submit" class="button search__button">
        {{ button }}
      </button>
    </form>
  </div>
</template>
  
<script>

export default {
  name: 'SearchVue',
  data () {
    return {
      placeholder: 'Поиск по названию картины',
      button: 'Найти'
    }
  }
}

</script>

<style scoped lang="scss">
  .search {
    &__form {
      display: flex;
      align-items: center;
    }
    &__input {
      border: 1px solid #E1E1E1;
      padding: 13px 16px;
      color: #343030;
      min-width: 294px;
      width: 100%;
      font-size: 14px;
      line-height: 21px;

      &:focus {
        border: 1px solid #B5B5B5;
        outline: 0;
      }
    }
  }

  @media all and (max-width: 1259px) {
    .search {
      &__input {
        min-width: auto;
        max-width: 200px;
      }
    }
  }
</style>