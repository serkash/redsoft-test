<template>
    <div class="painting" :class="(forSale) ? '' : 'painting_sold'">
      <div class="painting__image" :style="(image) ? `background-image: url(${image})` : ''"></div>
      <div class="painting__info">
        <span class="painting__title h2" v-if="title">
          {{ title }}
        </span>

        <div class="painting__info-bottom" v-if="forSale">
          <div class="painting__prices">
            <span class="painting__old-price h6" v-if="oldPrice">
              {{ oldPrice }}
            </span>
            <span class="painting__price h3">
              {{ price }}
            </span>
          </div>
          <button class="button painting__cart" :class="buttonClass" @click="addToCart">
            <div class="painting__loading" v-if="isLoading"></div>
            <span class="button__text" v-if="!isAddedToCart">{{ button }}</span>
            <span class="painting__added-to-cart" v-else>
              <img :src="featherIcon">
              <span class="button__text">{{ addedToCartText }}</span>
            </span>
          </button>
        </div>
        
        <div class="painting__info-bottom" v-else>
          <span class="painting__warning h3">
            {{ sold }}
          </span>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  
  export default {
    name: 'PaintingVue',
    props: {
      id: {
        type: Number,
        default: null
      },
      image: {
        type: String,
        default: ''
      },
      title: {
        type: String,
        default: ''
      },
      oldPrice: {
        type: String,
        default: ''
      },
      price: {
        type: String,
        default: ''
      },
      forSale: {
        type: Boolean,
        default: true
      }
    },
    data () {
      return {
        isLoading: false,
        isAddedToCart: false,
        buttonClass: null,
        featherIcon: require('@/assets/icons/feather.svg'),
        button: 'Купить',
        addedToCartText: 'В корзине',
        sold: 'Продана на аукционе',
        axiosJSON: null
      }
    },
    mounted () {
      this.checkPaintings()
    },
    methods: {
      checkPaintings () {
        const cart = JSON.parse(localStorage.getItem('cart'))
        if (cart && cart.includes(this.id)) {
          this.isAddedToCart = true
          this.buttonClass = 'painting__cart_added'
        }
      },
      addToCart () {
        if (this.isAddedToCart === false) {
          let cart = JSON.parse(localStorage.getItem('cart'))
          if (!cart) {
            cart = []
          }
          this.buttonClass = 'painting__cart_loading'
          this.isLoading = true
          this.axios
            .get('https://jsonplaceholder.typicode.com/posts/1')
            .then(response => {
              if (response) {
                cart.push(this.id)
                localStorage.setItem('cart', JSON.stringify(cart))
                this.isLoading = false
                this.isAddedToCart = true
                this.buttonClass = 'painting__cart_added'
              } else {
                this.isLoading = false
                this.buttonClass = null
              }
            })
        }
      }
    }
  }
  
</script>

<style scoped lang="scss">
  @keyframes painting-loading {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
  .painting {
    border: 1px solid #E1E1E1;

    &_sold {
      opacity: 0.5;
    }

    &__image {
      width: 100%;
      min-height: 160px;
      background: #ECEAEA no-repeat center center / cover;
    }

    &__info {
      padding: 24px;
      min-height: 172px;

      &-bottom {
        margin-top: 23px;
        min-height: 49px;
        display: flex;
        align-items: center;
        justify-content: space-between;
      }
    }

    &__prices {
      display: flex;
      flex-direction: column;
    }

    &__cart {
      &_loading {
        position: relative;

        & .button__text {
          opacity: 0;
        }
      }

      &_added {
        padding: 14px 8px;
      }
    }

    &__old-price {
      text-decoration: line-through;
      color: #A0A0A0;
    }

    &__loading {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      display: inline-block;
      width: 20px;
      height: 20px;

      &::after {
        content: " ";
        display: block;
        width: 12px;
        height: 12px;
        margin: 2px;
        border-radius: 50%;
        border: 2px solid #fff;
        border-color: #fff transparent #fff transparent;
        animation: painting-loading 1.2s linear infinite;
      }
    }

    &__added-to-cart {
      & img {
        margin-right: 4px;
      }
    }

  }
</style>