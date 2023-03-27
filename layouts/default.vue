<template>
  <v-app>
      <Nuxt />
  </v-app>
</template>

<script>
import fetch from "node-fetch";
export default {

}
</script>

<style>
* {
   scroll-behavior: smooth; /* Закоментить если хотеть без плавности */
}
.product-popup {
  background: white !important;
  max-width: 390px;
  padding: 9px 15px 22px 15px;
  align-self: flex-end  !important;
  margin: 0 !important;
}
@media screen and (max-width: 600px) {
  .product-popup {
    max-width: 100%;
  }
}
@media screen and (min-width: 1000px) {
  .product-popup {
    max-width: 600px;
    align-self: unset  !important;
  }
  /* .banner {
    opacity: 0;
    padding-top: -200px;
  } */
  .modal-line {
    opacity: 0;
  }
}
</style>
