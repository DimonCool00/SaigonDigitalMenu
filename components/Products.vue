<template>
  <div class="products">
    <div class="search-component">
      <input type="search" class="search-component__input" placeholder="Поиск..." @keyup="search"/>
      <svg width="17" height="17" class="search-component__icon">
        <use href="@/assets/icons/icons.svg#search-icon"></use>
      </svg>
    </div>
    <ProductItem v-for="(product, index) in products" :key="product.id" :product="product" :showPopup="showPopup"/>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        products: [],
        showModal: false,
        accessToken: '',
        showPopup: false
      }
    },
    created() {
        this.getAuthToken();
    },
    mounted() {

    },
    methods: {
      search(event) {
        this.getRestaurantProducts(event.target.value, true)
        this.$forceUpdate()
      },
      getAuthToken() {
        const body = {
          appName: "menu.rst.ozo.direct",
        };
        const options = {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(body),
        };
        fetch("/api/Auth/GetApplicationToken", options)
          .then((response) => {
            if (!response.ok) {
              throw new Error("Failed to get auth token");
            }
            return response.json();
          })
          .then((data) => {
            localStorage.setItem('accessToken', data?.accessToken);
            this.getRestaurantProducts('', false)
          })
          .catch((error) => {
            console.error(error);
          });
      },
      getRestaurantProducts(event, bool) {
        const url = `/api/product/GetRestaurantProducts?restaurantId=55DE9A40-561E-4F44-9AFF-9A8D048165FA`;
        const options = {
          headers: {
            Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
            "Content-Type": "application/json",
            "Access-Control-Allow-Origin": "*",
            "Access-Control-Allow-Methods": "GET, POST, PUT, DELETE, OPTIONS",
            "Access-Control-Allow-Headers":
              "Origin, X-Requested-With, Content-Type, Accept, Authorization",
          },
        };
        fetch(url, options)
          .then((response) => {
            if (!response.ok) {
              throw new Error("Failed to get restaurant products");
            }
            return response.json();
          })
          .then((data) => {
            if(bool) {
              this.products = data.filter(item => {
                if(item.name.includes(event) || item.name.toUpperCase().includes(event) || item.name.toLowerCase().includes(event)) {
                  return item
                }
              });
            }
            else this.products = data
          })
          .catch((error) => {
            console.error(error);
          });
    },
    }
  }
</script>

<style lang="scss" scoped>
.search-component {
  max-width: 390px;
  width: 100%;
  height: 40px;
  margin: 0 auto;

  display: flex;
  position: relative;

  &__input {
    background: #F0F1F3;
    border-radius: 8px;
    width: 100%;
    outline: unset;

    padding:0 40px;

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
</style>
