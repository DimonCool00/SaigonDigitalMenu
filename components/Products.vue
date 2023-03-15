<template>
  <div class="products">
    123
    <div v-for="(product, index) in products" :key="product?.id" @click="openModal">
      <img v-if="product.imagePath" :src="product.imagePath" alt="productImage"/>
      <img v-else src="" alt="defaultImage"/>
      <v-dialog content-class="product-dialog">
        <p>{{product?.title}}</p>
        <button @click="closeModal">
          Закрыть
        </button>
      </v-dialog>
     </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        products: [],
        showModal: false,
        accessToken: ''
      }
    },
    created() {
        this.getAccessToken();
    },
    mounted() {

    },
    methods: {
      openModal() {
        this.showModal = true
      },
      closeModal() {
        this.showModal = false
      },
    async getAccessToken() {
        await this.$axios.post('https://testapi.rst.ozo.direct/api/Auth/GetApplicationToken').then(res => console.log(res)).catch(err => console.error(err))
      }
    }
  }
</script>
