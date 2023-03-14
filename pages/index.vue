<template>
    <div class="page">
      <mobile-app-banner></mobile-app-banner>
      <header-main></header-main>
      <product-card></product-card>
      <menu-list></menu-list>
      <menu-list></menu-list>
      <menu-list></menu-list>
      <menu-list></menu-list>
      <menu-list></menu-list>
      <menu-list></menu-list>
      <menu-list></menu-list>
      <menu-list></menu-list>
      <menu-list></menu-list>
      <menu-list></menu-list>
      <menu-list></menu-list>
      <div id="menuitem-8"
      >
      <menu-list></menu-list>
    </div>
    <footer-main></footer-main>
    </div>
</template>

<script>

import Tutorial from '../components/Tutorial.vue';
import MobileAppBanner from '@/components/MobileAppBanner.vue'
import HeaderMain from '../components/HeaderMain.vue';
import MenuList from '../components/MenuList.vue';
import FooterMain from '../components/FooterMain.vue';
import ProductCardVue from '../components/ProductCard.vue';

export default {
  name: 'IndexPage',
  components: {
    MobileAppBanner,
    HeaderMain,
    MenuList,
    FooterMain,
    ProductCardVue
  },

}
</script>
