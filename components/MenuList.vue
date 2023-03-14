<template>
    <div>
        <!-- <HeaderMain  v-model="searchText"/> -->
        <div @click="showModal = true">
            <p class="category-header">Завтраки</p>
            <div class="product-card">
                <div class="product-image" >
                    <img src="https://testapi.rst.ozo.direct/Image/ProductBase/5da959c6-ae90-ed11-9cf0-0050560106ef/771bc6c7-abf2-4821-4299-08db02e583bb.jpeg" alt="Product Image">
                </div>
                <div class="product-details">
                    <h2 class="product-title">Деревенский Завтрак</h2>
                    <p class="product-description">Глазунья из 2-х яиц, сосиски Охотничьи, молодой картофель, микс салата, тост</p>
                <div class="product-button">
                        <span class="price">2 980 ₸</span>
                    </div>
            </div>
            </div>
        </div>
        <div class="product-card">
        <div class="product-image" >
            <img src="~/assets/product1.png" alt="Product Image">
        </div>
        <div class="product-details">
                <h2 class="product-title">Деревенский Завтрак</h2>
                <p class="product-description">Глазунья из 2-х яиц, сосиски Охотничьи, молодой картофель, микс салата, тост</p>
                <div class="product-button">
                    <span class="price">2 980 ₸</span>
                </div>
                <!-- <button class="product-button">2 980 ₸</button> -->
            </div>
        </div>
        <div class="product-card">
        <div class="product-image" >
            <img src="~/assets/product1.png" alt="Product Image">
        </div>
        <div class="product-details">
                <h2 class="product-title">Деревенский Завтрак</h2>
                <p class="product-description">Глазунья из 2-х яиц, сосиски Охотничьи, молодой картофель, микс салата, тост</p>
                <div class="product-button">
                    <span class="price">2 980 ₸</span>
                </div>
                <!-- <button class="product-button">2 980 ₸</button> -->
            </div>
        </div>
        <div class="product-card">
        <div class="product-image" >
            <img src="~/assets/product1.png" alt="Product Image">
        </div>
        <div class="product-details">
                <h2 class="product-title">Деревенский Завтрак</h2>
                <p class="product-description">Глазунья из 2-х яиц, сосиски Охотничьи, молодой картофель, микс салата, тост</p>
                <div class="product-button">
                    <span class="price">2 980 ₸</span>
                </div>
                <!-- <button class="product-button">2 980 ₸</button> -->
            </div>
        </div>
        <div class="product-card">
        <div class="product-image" >
            <img src="~/assets/product1.png" alt="Product Image">
        </div>
        <div class="product-details">
                <h2 class="product-title">Деревенский Завтрак</h2>
                <p class="product-description">Глазунья из 2-х яиц, сосиски Охотничьи, молодой картофель, микс салата, тост</p>
                <div class="product-button">
                    <span class="price">2 980 ₸</span>
                </div>
                <!-- <button class="product-button">2 980 ₸</button> -->
            </div>
        </div>
        <div class="overlay" v-if="showModal" @click="closeModal"></div>
        <div class="modal" v-if="showModal" @click.self="closeModal">
            <div class="popup-content">
                <div class="modal-line"  @click="closeModal"></div>
                <div class="modal-header">
                    <p class="modal-header-category">Завтраки</p>
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
        </div>
    </div>
  </template>
  
  <script>

    import HeaderMain from './HeaderMain.vue';
    import ProductCard from './ProductCard.vue';

  export default {
    props: {
    //   product: {
    //     id: 1,
    //     title: 'Aвокадо',
    //     description: 'This is the description of product 1',
    //     price: 100.00,
    //     image: 'product1.jpg',
    //     // required: true
    //   }
    },
    components : {
        HeaderMain,
        ProductCard,
    },
    data() {
      return {
        showModal: false,
        searchText: '',
        product: {
        title: 'Название продукта',
        description: 'Описание продукта'
      }
      }
    },
    methods: {
      goToProductPage() {
        // redirect user to product page
      },
    openModal() {
      this.$emit("open-modal");
    },
    closeModal() {
      this.showModal = false;
    }
    },
    // mounted() {
    //   if (window.innerWidth > 768) {
    //     this.showImage = false;
    //   }
    // }
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
  .product-card {
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: 1px;
    padding: 9px 35px 10px 18px;
    /* height: 150px; */
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
  align-items: stretch; /* Расстгиявате картинку по контейнеру */
}

.product-image img {
  max-width: 100%;
  height: auto;
  border-radius: 5px;  /* делаем изображение адаптивным */
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