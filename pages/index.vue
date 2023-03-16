<template>
  <main>
    <mobile-app-banner></mobile-app-banner>
    <VueHeader />
    <Products />
  </main>
</template>


<script>
import Products from "~/components/Products.vue";
import VueHeader from '~/components/ui/vueHeader.vue';
import MobileAppBanner from "../components/MobileAppBanner.vue";
export default {
  components: {
    Products,
    VueHeader,
    MobileAppBanner
  }
}
</script>
