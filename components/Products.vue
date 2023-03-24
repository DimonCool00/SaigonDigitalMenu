<template>
  <div class="products">
    <vm-back-top :duration="250"></vm-back-top>
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
      :duration="150"
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
    <!-- Для отображения данного сообщения   -->
    <div v-if="message" class="search-notfound">{{ message }}</div>
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

    // Фильтрация где просто выподиться пустой белый экран
    // filteredItems() {
    //  return Object.fromEntries(
    //     Object.entries(this.items).map(([key, value]) => {
    //       if (value) {
    //         return [
    //           key,
    //           value.filter(({ name }) => name.toLowerCase().includes(this.search.toLowerCase())) 
    //         ];
    //       }
    //     })
    //   );
      
    // },

    //Фильтрация с сообщением 
    filteredItems() {
      const filtered = Object.fromEntries(
        Object.entries(this.items).map(([key, value]) => {
          if (value) {
            const filteredValue = value.filter(({ name }) =>
              name.toLowerCase().includes(this.search.toLowerCase())
            );
            return [key, filteredValue];
          }
          return [key, []];
        })
      );
      const hasResults = Object.values(filtered).some((value) => value.length > 0);
      this.message = hasResults ? " " : "По вашему запросу ничего не найдено."; // устанавливаем сообщение в зависимости от наличия результатов
      return filtered;
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
.search-notfound {
    // display: flex;
    margin: 0 auto;
    font-family: 'Inter';
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 22px;
    
}
.search-component {
  max-width: 390px;
  width: 100%;
  height: 40px;
  // margin: 0 auto;
  margin: 0 auto;
  display: flex;
  position: relative;
  flex-direction: row;

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
  margin: 10px -25px 20px -18px;
  // margin-top: 20px;
  box-shadow: 0px 3px 0px rgba(137, 113, 113, 0.09);
  height: 45px;
  padding: 0 0 0 15px !important;
  body::-webkit-scrollbar {
    display: none;
  }

  a {
    padding: 6px 9px;
    margin-right: 12px;
    text-decoration: none;
    cursor: pointer;
    .scrollactive-item:first-child {
      margin-left: 5px;
    }
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
  padding: 0 25px 0 18px;
  min-height: 600px;
}
:deep(.vm-back-top-inner:hover) {
  background-color: #E40613;
  border-radius: 50%;
  box-shadow: 0 1px 3px rgb(0 0 0 / 20%);
  transition: all 0.2s ease-in-out;
  width: 100%;
  height: 100%;
}
:deep(.vm-back-top-inner) {
  background-color: #E40613;
  border-radius: 50%;
  box-shadow: 0 1px 3px rgb(0 0 0 / 20%);
  transition: all 0.2s ease-in-out;
  width: 100%;
  height: 100%;
}
:deep(.vm-back-top i) {
  color: #fff;
  font-size: 15px;
  padding: 10px 15px;
  /* border-radius: 50%; */
  /* padding: 20px; */
}
</style>
