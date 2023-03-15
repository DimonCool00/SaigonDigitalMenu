<template>
  <main>
    <VueHeader />
    <Products />
  </main>
</template>


<script>
import Products from "~/components/Products.vue";
import VueHeader from '~/components/ui/vueHeader.vue';
export default {
  components: {
    Products,
    VueHeader
  }
}
</script>
