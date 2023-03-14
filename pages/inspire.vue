<template>
  <v-row>
    <v-col class="text-center">
      <img
        src="/v.png"
        alt="Vuetify.js"
        class="mb-5"
      >
      <blockquote class="blockquote">
        &#8220;First, solve the problem. Then, write the code.&#8221;
        <footer>
          <small>
            <em>&mdash;John Johnson</em>
          </small>
        </footer>
      </blockquote>
      <div class="page">
      <!-- ... -->
      <mobile-app-banner></mobile-app-banner>
    </div>
    </v-col>
  </v-row>
</template>

<script>
import MobileAppBanner from '@/components/MobileAppBanner.vue';

export default {
  name: 'InspirePage',
  components: {
    MobileAppBanner,
  },
}
</script>
