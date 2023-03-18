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
  scroll-behavior: smooth;
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
</style>
