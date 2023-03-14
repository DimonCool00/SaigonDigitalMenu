  <template>
    <div>
        <div class="overlay" @click="$emit('close-modal')"></div>
        <div class="modal" @click.self="closeModal">
            <div class="popup-content">
                <div class="modal-line"  @click="$emit('close')"></div>
                <div class="modal-header">
                    <p class="modal-header-category">{{ product.categoryheader }}</p>
                    <div class="close-modal-button">
                        <span class="close-modal" @click="$emit('close')" style="color: #9F9F9F; width: 11px; height: 11px;">×</span>
                    </div>
                </div>
                <div class="product-image-modal">
                    <img :src="`https://testapi.rst.ozo.direct${product.images[0].imagePath}`" alt="Product Image">
                </div>
                <div class="product-detail-modal">
                    <button @click="$emit('close')">Закрыть</button>
                    <h2 class="product-title-modal">{{ product.name }}</h2>
                <p class="product-description-modal">{{ product.description }}</p>
                </div>
            </div>
        </div>
    </div>
  </template>
  
  <script>
  export default {
        props: {
        product: {
        type: Object,
        required: true,
        },
    },
    data() {
      return {
      };
    },
    methods: {
    openModal() {
      this.$emit("open-modal");
    },
    closeModal() {
      this.showModal = false;
    },
    },
  };
  </script>
  
  <style>
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
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 998;
}
</style>
