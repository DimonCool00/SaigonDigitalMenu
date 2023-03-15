<template>
  <div class="product-item" @click="openModal">
    <div class="image">
    <svg width="136" height="136">
      <use href="@/assets/icons/icons.svg#product-image"></use>
    </svg>
    </div>
    <div class="d-flex flex-column justify-space-between fill-height product-item__content">
      <h3>{{product.name}}</h3>
      <span>{{product.description}}</span>
      <button @click="price(product)">
        {{product.price}}
      </button>
    </div>
    <v-dialog content-class="product-popup" v-model="showPopup">
      <div class="product-popup__header">
        <h2>Завтраки</h2>
        <svg @click="closeModal" class="close" width="30" height="30" viewBox="0 0 30 30" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path fill-rule="evenodd" clip-rule="evenodd" d="M15 30C23.2843 30 30 23.2843 30 15C30 6.71573 23.2843 0 15 0C6.71573 0 0 6.71573 0 15C0 23.2843 6.71573 30 15 30Z" fill="#EFEFEF"/>
          <path d="M9.90625 19C9.52344 19.375 9.51562 20.0625 9.91406 20.4609C10.3125 20.8594 11 20.8438 11.375 20.4688L15 16.8438L18.625 20.4609C19.0156 20.8516 19.6875 20.8594 20.0859 20.4531C20.4844 20.0547 20.4844 19.3828 20.0938 18.9922L16.4766 15.375L20.0938 11.75C20.4844 11.3594 20.4844 10.6875 20.0859 10.2891C19.6875 9.88281 19.0156 9.89062 18.625 10.2812L15 13.8984L11.375 10.2734C11 9.89844 10.3125 9.88281 9.91406 10.2812C9.51562 10.6797 9.52344 11.3672 9.90625 11.75L13.5312 15.375L9.90625 19Z" fill="#9F9F9F"/>
        </svg>

      </div>
      <div class="product-popup__content">
        <svg width="136" height="136">
          <use href="@/assets/icons/icons.svg#product-image"></use>
        </svg>
        <h3 class="product-popup__title">
          {{product.name}}
        </h3>
        <span class="product-popup__description">
          {{product.description}}
        </span>
      </div>
    </v-dialog>
   </div>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      default: {}
    },
  },
  data() {
      return {
        showPopup: false,
      }
  },
  methods: {
    price(product) {
      console.log(product)
    },
    openModal() {
      this.showPopup = true
    },
    closeModal() {
      this.showPopup = false
    }
  }
}
</script>

<style lang="scss" scoped>

.image {
  max-width: 136px;
  width: 100%;
  margin-right: 13px;
svg {
  border-radius: 5px;
  object-fit: cover;
}
}
.product-item {
  display: flex;
  align-items: center;
  max-width: 390px;
  margin-bottom: 30px;
  padding: 0 16px;
  max-height: 136px;
  height: 100%;

  &__content {
  height: 136px;
  }

  &:last-of-type {
    margin-bottom: 0;
  }

  h3 {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 600;
    font-size: 16px;
    line-height: 19px;
    color: #383838;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -moz-box;
    -moz-box-orient: vertical;
    display: -webkit-box;
    -webkit-line-clamp: 1;
    -webkit-box-orient: vertical;
    line-clamp: 3;
    box-orient: vertical;
  }
  span {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 17px;
    color: #9F9F9F;
    margin: 5px 0;

    overflow: hidden;
    text-overflow: ellipsis;
    display: -moz-box;
    -moz-box-orient: vertical;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    line-clamp: 5;
    box-orient: vertical;
  }

  button {
    width: 107px;
    height: 35px;
    background: #F0F1F3;
    border-radius: 5px;

    display: flex;
    align-items: center;
    justify-content: center;

    font-family: 'Inter';
    font-style: normal;
    font-weight: 600;
    font-size: 16px;
    line-height: 19px;
    text-align: center;
  }
}
.close {
  cursor: pointer;
  border-radius: 50%;
}
.product-popup {
  display: flex;
  flex-direction: column;
  align-items: center;
  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  &__image {
    width: 100% !important;
    object-fit: cover;
    margin: 18px 0;
  }
}
</style>
