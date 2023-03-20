<template>
  <div class="d-flex flex-column w390" v-if="products.length">
    <h3 class="category-name">{{ categoryName }}</h3>
    <div class="mt-4 d-flex flex-column">
      <div
        class="product-item d-flex"
        v-for="product in products"
        :key="product.name"
        @click="openModal(product)"
      >
        <img
          v-if="product.images.length && product.images[0]"
          :src="`https://testapi.rst.ozo.direct${product.images[0].imagePath}`"
          class="product-item__image"
        />
        <img v-else src="@/assets/images/notload.png" class="product-item__image" />
        <div class="product-item__details d-flex flex-column justify-space-between">
          <h3>{{ product.name }}</h3>
          <span>{{ product.description }}</span>
          <button @click="price(product)">{{ product.price }} ₸</button>
        </div>
      </div>
    </div>
    <v-dialog v-if="selectedProduct.images" content-class="product-popup" v-model="showPopup">
      <div class="modal-line d-flex align-center" @click="closeModal"></div>
      <div class="product-popup__header d-flex justify-space-between align-center">
        <h2 class="product-popup__category">{{ categoryName }}</h2>
        <svg
          @click="closeModal"
          class="close"
          width="30"
          height="30"
          viewBox="0 0 30 30"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M15 30C23.2843 30 30 23.2843 30 15C30 6.71573 23.2843 0 15 0C6.71573 0 0 6.71573 0 15C0 23.2843 6.71573 30 15 30Z"
            fill="#EFEFEF"
          />
          <path
            d="M9.90625 19C9.52344 19.375 9.51562 20.0625 9.91406 20.4609C10.3125 20.8594 11 20.8438 11.375 20.4688L15 16.8438L18.625 20.4609C19.0156 20.8516 19.6875 20.8594 20.0859 20.4531C20.4844 20.0547 20.4844 19.3828 20.0938 18.9922L16.4766 15.375L20.0938 11.75C20.4844 11.3594 20.4844 10.6875 20.0859 10.2891C19.6875 9.88281 19.0156 9.89062 18.625 10.2812L15 13.8984L11.375 10.2734C11 9.89844 10.3125 9.88281 9.91406 10.2812C9.51562 10.6797 9.52344 11.3672 9.90625 11.75L13.5312 15.375L9.90625 19Z"
            fill="#9F9F9F"
          />
        </svg>
      </div>
      <div class="product-popup__content">
        <img
          v-if="selectedProduct.images.length && selectedProduct.images[0]"
          :src="`https://testapi.rst.ozo.direct${selectedProduct.images[0].imagePath}`"
        />
        <img v-else src="@/assets/images/notload.png" />
        <h3 class="product-popup__title mb-3 mt-6">
          {{ selectedProduct.name }}
        </h3>
        <span class="product-popup__description">
          {{ selectedProduct.description }}
        </span>
      </div>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: {
    products: {
      type: Array,
      default: [],
    },
    categoryName: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      showPopup: false,
      selectedProduct: {},
    };
  },
  methods: {
    price(product) {
      console.log(product);
    },
    openModal(item) {
      this.showPopup = true;
      this.selectedProduct = item;
    },
    closeModal() {
      this.showPopup = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.w390 {
  max-width: 390px;
  width: 100%;
  margin-bottom: 35px;
}
.modal-line {
  background: #cdcdcd;
  border-radius: 10px;
  border: 1px;
  height: 5px;
  width: 39px;
  display: flex;
  align-items: center;
  text-align: center;
  margin: auto;
  margin-bottom: 5px;
}
.category-name {
  font-family: 'Inter';
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 22px;
  color: #383838;
  margin-bottom: 0px;
}
.product-item {
  margin-bottom: 10px;
  &:last-of-type {
    margin-bottom: 0;
  }
  &__image {
    max-width: 136px;
    width: 100%;
    height: 136px;
    border-radius: 8px;
    margin-right: 13px;
    object-fit: cover;
  }
  &__details {
    h3 {
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
      overflow: hidden;
    }
    span {
      display: -webkit-box;
      -webkit-line-clamp: 3;
      -webkit-box-orient: vertical;
      overflow: hidden;
      margin: 5px;
      font-family: 'Inter';
      font-style: normal;
      font-weight: 400;
      font-size: 14px;
      line-height: 17px;
      color: #9f9f9f;
    }
    button {
      background: #f0f1f3;
      border-radius: 5px;
      max-width: 107px;
      width: 100%;
      height: 35px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: 'Inter';
      font-style: normal;
      font-weight: 600;
      font-size: 16px;
      line-height: 19px;
      text-align: center;
      color: #383838;
    }
  }
}
.product-popup {
  &__category {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    line-height: 22px;
    display: flex;
    align-items: center;
    color: #383838;
  }
  &__title {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    line-height: 22px;
    display: flex;
    align-items: center;
    color: #383838;
  }
  &__description {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 19px;
    display: flex;
    align-items: center;
    color: #5e5e5e;
  }
  &__content {
    margin-top: 15px;
    img {
      border-radius: 8px;
      width: 100%;
      max-height: 273px;
      height: auto;
      object-fit: cover;
    }
  }
}
</style>
