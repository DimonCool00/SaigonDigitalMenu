<template>
  <div class="products">
    <div class="search-component">
      <input
        type="search"
        class="search-component__input"
        v-model="search"
        placeholder="Поиск..."
      />
      <svg width="17" height="17" class="search-component__icon">
        <use href="@/assets/icons/icons.svg#search-icon"></use>
      </svg>
    </div>

    <scrollactive class="navigation d-flex align-center"
      v-on:itemchanged="onItemChanged"
      active-class="active"
      :modifyUrl="false"
      :offset="80"
      :duration="800"
      bezier-easing-value=".5,0,.35,1"
    >
      <a
        class="scrollactive-item"
        v-for="category in filteredCategories"
        :key="category.id"
        :href="'#' + category.id"
      >
        <h3 v-text="category.name"></h3>
      </a>
    </scrollactive>

    <ProductItem
      v-for="[categoryId, products], idx in Object.entries(filteredItems)"
      :key="idx"
      :id="categoryId"
      :products="products"
      :categoryName="getCategoryMeta(categoryId).name"
      :showPopup="showPopup"
    />
  </div>
</template>

<script>
export default {

  data() {
    return {
      products: [],
      showModal: false,
      accessToken: '',
      showPopup: false,
      search: '',
      categories: [],
    };
  },
  async created() {
    await this.init();
  },
  computed: {
    filteredCategories() {
      return this.categories.filter(({ id }) => this.items[id].length);
    },

    items() {
      const products = this.products.reduce((acc, product) => ({
        ...acc,
        [product.categoryId]: [
          ...(acc[product.categoryId] ?
          [...acc[product.categoryId], product] :
          [product])
        ],
      }), {});
      return this.categories.reduce((acc, { id }) => ({
        ...acc,
        [id]: products[id] || []
      }), {})
    },

    filteredItems() {
      return Object.fromEntries(
        Object.entries(this.items).map(([key, value]) => {
          if (value) {
            return [
              key,
              value.filter(({ name }) => name.toLowerCase().includes(this.search.toLowerCase()))
            ];
          }
        })
      )
    },
  },

  watch: {
    currentCategory() {
      // this.currentCategory.scrollTo({ behavior: 'smooth', inline: 'center' });
    }
  },

  methods: {
    onItemChanged(event, currentItem, lastActiveItem) {
    },
    async init() {
      await this.getAuthToken();
      await this.getRestaurantProducts();
      await this.getCategories();
    },

    getCategoryMeta(categoryId) {
      return this.categories.find(({ id }) => id == categoryId);
    },

    async getAuthToken() {
      const body = {
        appName: 'menu.rst.ozo.direct',
      };
      const options = {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(body),
      };
      try {
        const response = await fetch('/api/Auth/GetApplicationToken', options);
        const { accessToken } = await response.json();
        this.accessToken = accessToken;
      } catch (error) {
        console.error(error);
      }
    },
    async getRestaurantProducts() {
      const url = `/api/product/GetRestaurantProducts?restaurantId=55DE9A40-561E-4F44-9AFF-9A8D048165FA`;
      const options = {
        headers: {
          Authorization: `Bearer ${this.accessToken}`,
          'Content-Type': 'application/json',
          'Access-Control-Allow-Origin': '*',
          'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
          'Access-Control-Allow-Headers':
            'Origin, X-Requested-With, Content-Type, Accept, Authorization',
        },
      };
      try {
        const response = await fetch(url, options);
        if (!response.ok) {
          throw new Error('Failed to get restaurant products');
        }
        const data = await response.json();
        this.products = data;
      } catch (error) {
        console.error(error);
      }
    },
    async getCategories() {
      const url = `/api/Category/GetRestaurantCategories?restaurantId=55DE9A40-561E-4F44-9AFF-9A8D048165FA`;
      const options = {
        headers: {
          Authorization: `Bearer ${this.accessToken}`,
          'Content-Type': 'application/json',
          'Access-Control-Allow-Origin': '*',
          'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
          'Access-Control-Allow-Headers':
            'Origin, X-Requested-With, Content-Type, Accept, Authorization',
        },
      };
      try {
        const response = await fetch(url, options);
        if (!response.ok) {
          throw new Error('Failed to get restaurant products');
        }
        const data = await response.json();
        this.categories = data;
      } catch (error) {
        console.error(error);
      }
    },
  },

  mounted() {
    window.addEventListener('scroll', () => {
      const el = document.querySelector('.scrollactive-item.active');
      if (el) {
        this.$nextTick(() => {
          el.scrollIntoViewIfNeeded({ behavior: 'smooth', inline: 'center' });
        })
      }
    });
  },
};
</script>

<style lang="scss" scoped>
.navigation::-webkit-scrollbar {
  height: 0px;
  background-color: #ffffff;
}
.navigation::-webkit-scrollbar-thumb {
  background-color: #ffffff;
}
.search-component {
  max-width: 390px;
  width: 100%;
  height: 40px;
  margin: 0 auto;

  display: flex;
  position: relative;

  &__input {
    background: #f0f1f3;
    border-radius: 5px;
    width: 100%;
    outline: unset;

    padding: 0 40px;

    display: flex;
    align-items: center;
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 18px;
    line-height: 22px;
  }

  &__icon {
    position: absolute;
    top: 11.5px;
    left: 12px;
  }
}
.navigation {
  position: sticky;
  top: -1px; // 0
  background: #ffffff;
  overflow-x: scroll;
  margin: 10px 0 20px;
  // margin-top: 20px;
  box-shadow: 0px 3px 0px rgba(137, 113, 113, 0.09);
  height: 45px;
  padding: 0 0 0 5px !important;
  body::-webkit-scrollbar {
    display: none;
  }

  a {
    padding: 6px 9px;
    margin-right: 12px;
    text-decoration: none;
    cursor: pointer;
    h3 {
      width: max-content;
      font-family: 'Inter';
      font-style: normal;
      font-weight: 400;
      font-size: 16px;
      line-height: 19px;
      text-align: center;
      color: #383838;
      flex: none;
      order: 0;
      flex-grow: 0;
      margin-right: 20px;

      &:last-of-type {
        margin-right: 0;
      }
    }
  }
}
.active {
  background: #5e5e5e;
  border-radius: 5px;

  h3 {
    color: white !important;
  }
}
.products {
  padding: 0 12px;
}
</style>
