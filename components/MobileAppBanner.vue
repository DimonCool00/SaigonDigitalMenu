<template>
  <div class="banner d-flex align-center justify-center" v-if="showBanner">
    <span class="close" @click="hideBanner">×</span>
    <div class="content">
      <img src="../assets/Android.png" alt="Мобильное приложение" class="img" />
      <div class="text">
        <p class="banner_header">Заказывайте в приложении</p>
        <p class="banner_text">
          Оформляйте доставку, получайте бонусы и подарки
        </p>
      </div>
      <button class="btn" @click.prevent="downloadApp">СКАЧАТЬ</button>
    </div>
  </div>
</template>

<style scoped>
.banner {
  position: relative;
  top: 0;
  background-color: #f2f2f2;
  padding: 0 15px 0 10px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
}

.content {
  display: flex;
  align-items: center;
  /* width: 100%;  */
  margin: 0 auto;
}

.img {
  width: 56px;
  height: 56px;
  margin: 11px 8px;
}

.text {
  margin: 0px;
}

.btn {
  background-color: none;
  color: #0a7aff;
  border: none;
  padding: 28px 15px 31px 15px;
  font-family: "Inter";
  font-style: normal;
  cursor: pointer;
  font-weight: 400;
  font-size: 14px;
  line-height: 17px;
}
.banner_header {
  font-family: "Inter";
  font-style: normal;
  font-weight: 700;
  font-size: 14px;
  line-height: 17px;
  display: flex;
  align-items: center;
  color: #000000;
  margin-bottom: 0px;
}
.banner_text {
  color: #383838;
  font-family: "Inter";
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  display: flex;
  align-items: center;
  margin-bottom: 0px;
}
.close {
  font-size: 20px;
  cursor: pointer;
  color: #9f9f9f;
}
</style>
<script>
export default {
  name: "MobileAppBanner",
  data() {
    return {
      showBanner: true,
    };
  },
  methods: {
    hideBanner() {
      this.showBanner = false;
    },
    downloadApp() {
      if (/Android/i.test(navigator.userAgent)) {
        // Отображение ссылки для скачивания приложения Vue.js для Android
      } else if (/iPhone|iPad|iPod/i.test(navigator.userAgent)) {
        // Отображение ссылки для скачивания приложения Vue.js для iOS
      } else {
        // Отображение ссылки для скачивания приложения Vue.js для других устройств
      }
    },
  },
};
</script>
