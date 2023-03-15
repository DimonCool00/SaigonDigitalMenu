<template>
    <div>
            <div v-for="(product, index) in products" :key="product.id">
              <p сlass="category-header"   v-if="index > 0 && product.category.name != products[index-1].category.name" 
              style="font-family: 'Inter';
              font-style: normal;
              font-weight: 400;
              font-size: 18px;
              line-height: 22px;
              color: #383838;
              margin: 18px 0 0 16px;">
              {{ product.category.name }}</p>
                <div class="product-card">
                    <div class="product-image" >
                        <img v-if="isImageLoaded && product.images && product.images[2] && product.images[2].imagePath" :src="`https://testapi.rst.ozo.direct${product.images[2].imagePath}`" alt="Product Image" @load="onImageLoad" @error="onImageError" >
                        <div v-else class="image-placeholder">
                            <p class="category-header">Failed to load Image</p>
                        </div>
                    </div>
                    <div class="product-details">
                        <h2 class="product-title">{{ product.name }}</h2>
                        <p class="product-description">{{ product.description }}</p>
                        <div :id="`menuitem-${index}`"></div>
                        <div class="product-button">
                            <span class="price">{{ product.price }} ₸</span>
                        </div>
                    </div>
                </div>
          </div>
        <!-- </div> -->
        <!-- <div class="overlay" v-if="showModal" @click="closeModal"></div>
        <div class="modal" v-if="showModal" @click.self="closeModal">
            <div class="popup-content">
                <div class="modal-line"  @click="closeModal"></div>
                <div class="modal-header">
                    <p class="modal-header-category">{{ product.categoryheader }}</p>
                    <div class="close-modal-button">
                        <span class="close-modal" @click="closeModal" style="color: #9F9F9F; width: 11px; height: 11px;">×</span>
                    </div>
                </div>
                <div class="product-image-modal">
                    <img src="~/assets/product-modal.png" alt="Product Image">
                </div>
                <div class="product-detail-modal">
                    <h2 class="product-title-modal">{{ product.title }}</h2>
                <p class="product-description-modal">{{ product.description }}</p>
                </div>
            </div>
        </div> -->
    </div>
  </template>
  
  <script>

    import ProductPopUp from './ProductPopUp.vue';

    export default {
    
    // components : {
    //     ProductPopUp,
    // },
    // props: {
    //     product: {
    //   type: Object,
    //   required: true,
    // },
    // },
    data() {
      return {
        // showModal: false,
        searchText: '',
        products: [],
        token: "",
        isImageLoaded: true,
      }
    },
    methods: {
    //     openModal() {
    //   this.$emit("open-modal");
    // },
    // closeModal() {
    //   this.showModal = false;
    // },
    onImageLoad() {
      this.isImageLoaded = true;
    },
    onImageError() {
      this.isImageLoaded = false;
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
          this.token = data.accessToken;
          console.log("Token:", this.token);
          this.getRestaurantProducts();
        })
        .catch((error) => {
          console.error(error);
        });
    },
    getRestaurantProducts() {
      const url = `/api/product/GetRestaurantProducts?restaurantId=55DE9A40-561E-4F44-9AFF-9A8D048165FA`;
      const options = {
        headers: {
          Authorization: `Bearer ${this.token}`,
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
          this.products = data;
          console.log("Products:", this.products);
          // console.log(this.products.category.name)
        })
        .catch((error) => {
          console.error(error);
        });
    },
    },
    
    mounted() {
        this.getAuthToken();
    },
    // mounted() {
    // axios.get('https://example.com/api/products')
    //   .then(response => {
    //     this.products = response.data;
    //   })
    //   .catch(error => {
    //     console.log(error);
    //   });
    // } ,
        computed: {
        filteredCards() {
        return this.product.title(card => {
            return card.title.toLowerCase().includes(this.searchText.toLowerCase());
        });
        },
    },
  }
  </script>
  
  <style scoped>
  .image-placeholder {
    max-width: 100%;
  height: auto;
  border-radius: 5px;
  object-fit: cover;
  background-color: #ccc; /* серый цвет, который вы хотите использовать */
  }  
  .product-card {
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: 1px;
    padding: 9px 35px 10px 18px;
    /* min-height: 145px;
    max-height: 145px; */
    /* margin: 10px; */
    
  }
  .overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 998;
}
  /* .product-image img {
    min-width: 100%;
    height: auto;

  } */
  .product-image {
  max-width: 136px;
  height: auto;
  display: flex;
  align-items: stretch; /* Расстгиявате картинку по контейнеру смотрится хорошо */
}
.product-image img {
  max-width: 100%;
  height: auto;
  border-radius: 5px;
  object-fit: cover;  /* делаем изображение адаптивным */
}
  .product-details {
    padding-left: 13px;
    justify-content: space-between;
    display: flex;
    flex-direction: column;
  }
  
  .product-title {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 600;
    font-size: 16px;
    line-height: 19px;
    color: #383838;
    height: 2.6em;
    overflow: hidden;
    text-overflow: ellipsis;
    /* display: -webkit-box; */
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
  }
  
  .product-description {
    margin-top: 5px;
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 17px;
    color: #9F9F9F;
    margin-bottom: 0px;
    height: 3.6em; 
    overflow: hidden; 
    text-overflow: ellipsis;
    display: -webkit-box; 
    -webkit-line-clamp: 3; 
    -webkit-box-orient: vertical;
  }
  
  .product-price {
    font-weight: bold;
    margin: 0;
  }
  .price-block {
  background-color: #F2F2F2; /* задаем цвет фона */
  border-radius: 5px; /* задаем радиус скругления углов */
  padding: 10px; /* задаем внутренний отступ */
  display: inline-block; /* устанавливаем блок в режим инлайн */
}
  
  .product-button {
    margin-top: 5px;
    background: #F0F1F3;
    border-radius: 5px;
    padding: 8px 24px 8px 23px;
    font-family: 'Inter';
    font-style: normal;
    font-weight: 600;
    font-size: 16px;
    line-height: 19px;
    text-align: center;
    color: #383838;
    max-width: 107px;
  }
  .category-header {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 18px;
    line-height: 22px;
    color: #383838;
    margin: 18px 0 0 16px;
  }
  /*--------------------------------------------- Modal */
  .modal {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: auto;
  background-color: white;
  z-index: 999;
  transition: all 0.3s ease-out;
}   
.popup-content {
    display: flex;
    align-items: center;
    flex-direction: column;
    padding: 9px 15px 0 15px;
}
.modal-header {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 100%;
}
.modal-header-category {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    line-height: 22px;
    color: #383838;
}
.close-modal-button {
    background: #EFEFEF;
    border-radius: 30px;
    width: 30px;
    height: 30px;
    text-align: center;
    padding: 3px;
}
.close-modal {
    cursor: pointer;
}
/* .product-image-modal img {
    width: 100%;
    height: auto;
    object-fit: contain;
} */
.product-image-modal {
  /* max-width: 136px; */
  display: flex;
  justify-content: center;
  /* object-fit: cover задаем максимальную ширину изображения */
}

.product-image-modal img {
    max-width: 100%;
    height: auto; 
}
.product-detail-modal {
    display: flex;
    flex-direction: column;
    float: left;

}
.product-title-modal {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    line-height: 22px;
    color: #383838;
    margin-top: 18px;
}
.product-description-modal {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 19px;
    color: #5E5E5E;
    margin-top: 12px;
    margin-bottom: 48px;
}
.modal-line {
    background: #CDCDCD;
    border-radius: 10px;
    border: 1px ;
    height: 5px;
    width: 39px;
}
  </style>