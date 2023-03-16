<template>
  <div class="products">
    <div class="search-component">
      <input type="search" class="search-component__input" placeholder="Поиск..." @keyup="search"/>
      <svg width="17" height="17" class="search-component__icon">
        <use href="@/assets/icons/icons.svg#search-icon"></use>
      </svg>
    </div>
    <div class="navigation d-flex align-center">
      <div v-for="item in categories" :key="categories.id" @click="selectCategory(item)" :class="{active: selectedCategory === item.name}">
        <h3>{{item.name}}</h3>
      </div>
    </div>
    <ProductItem v-for="(item) in categories" :key="item.id" :item="item" :showPopup="showPopup"/>
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
        categories: [],
        selectedCategory: null,
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
      selectCategory(item) {
        this.selectedCategory = item.name
        if(process.client) {document.getElementById(item.scrollId).scrollIntoView();
        }
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
            this.getCategories()
          })
          .catch((error) => {
            console.error(error);
          });
    },
      getCategories() {
        const url = `/api/Category/GetRestaurantCategories?restaurantId=55DE9A40-561E-4F44-9AFF-9A8D048165FA`;
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
          }).then(res => {
            if(this.products && this.products.length) {
              for (let i = 0; i < this.products.length; i++) {
                  for(let j =0; j < res.length; j++) {
                    if(res[j].id == this.products[i].categoryId) {
                      this.products[i].categoryName = res[j].name;
                      this.categories.push({
                        name: res[j].name,
                        id: res[j].id,
                        scrollId: `Category${j}`,
                        products: []
                      })
                      this.categories = this.categories.filter((v,i,a)=>a.findIndex(v2=>(v2.id===v.id))===i)
                    }
                  }
                    this.categories.forEach(item => {
                      if(item.id === this.products[i].categoryId) {
                        item.products.push({
                          name: this.products[i].name,
                          description: this.products[i].description,
                          images: this.products[i].images,
                          price: this.products[i].price
                        })
                      }
                    })
              }
              console.log(this.categories)
              // this.categories = this.categories.map(item => {
              //   return {
              //
              //   }
              // })
            }
            }
        )
      }
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
.navigation {
  overflow-x: scroll;
  margin: 23px 0 20px;
  body::-webkit-scrollbar {
    display: none;
  }

  div {
    padding: 6px 9px;
    margin-right: 12px;
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
  background: #5E5E5E;
  border-radius: 5px;

  h3 {
    color: white !important;
  }
}
.products {
  padding: 0 12px;
}
</style>
