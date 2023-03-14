<!-- Please remove this file from your project -->
<template>
    <div>
      <div class="d-sm-block d-mb-block d-lg-none">
        <div class="footer-mobile">
          <div class="footer__container-mobile">
            <div class="footer__logo-mobile logotype">
              <nuxt-link to="/" class="logotype__link"
                ><img class="logotype__image" src="~/assets/footer_logo.svg"
              /></nuxt-link>
              <div class="download-app">
                    <p class="mobile-app-download footer-text">
                        Скачать мобильное приложение
                    </p>
                    <div class="download-image-container">
                        <a href="ссылка1"><img src="~/assets/android_dow.svg"></a>
                        <a href="ссылка2"><img src="~/assets/ios_dow.svg"></a>
                    </div>
              </div>
              <div class="follow-us-block">
                    <p class="footer-text">
                        Подписаться на нас
                    </p>
                    <div class="follow-us-links">
                     <a href="ссылка1"><img src="~/assets/facebook.svg"></a>
                     <a href="ссылка2"><img src="~/assets/instagram.svg"></a>
                    </div>
                </div>
            </div>
            <div class="footer__navigation-mobile">
              <div class="footer-navigation__links-mobile">
                <nuxt-link
                  to="/policy.pdf"
                  target="_blank"
                  class=""
                  >Политика Конфиденциальности</nuxt-link
                >
                <nuxt-link
                  to="/policy.pdf"
                  target="_blank"
                  class=""
                  >Публичная Оферта</nuxt-link
                >
              </div>
              <div class="line" style="border: 1px solid #5E5E5E; margin-top: 22px;"></div>
            </div>
            <div class="ozo-direct">
                <p class="ozo-direct-text">
                    OZO.DIRECT
                </p>
            </div>
          </div>
        </div>
      </div>
      <!-- <div class="d-none d-lg-block d-xl-block d-xxl-block">
        <div class="footer">
          <div class="footer__container">
            <div class="footer__logo logotype">
              <nuxt-link to="/" class="logotype__link" href="#"
                ><img class="logotype__image" src="~/assets/footer_logo.svg"
              /></nuxt-link>
              <div class="footer-navigation__address address">
                <a class="address__link" style="text-decoration: none" href="">
                  <img src="" />
                  <p class="address__text">
                    117335, Москва ул. Вавилова д.97 комн 1
                  </p>
                </a>
                <a class="address__link" href="tel: +79257397945 "
                  ><img src="" />
                  <p class="address__text">+7 925 739 79 45</p>
                </a>
                <a
                  class="address__link"
                  href="mailto: info@comproducts.ru?subject=TestQuestion"
                  ><img src="" />
                  <p class="address__text">info@comproducts.ru</p>
                </a>
              </div>
            </div>
            <div class="footer__navigation">
              <div class="footer-navigation__links">
                <p @click="$emit('SiteCreate')" class="footer-text">
                  Создание сайтов
                </p>
                <p @click="$emit('SiteCreate')" class="footer-text">
                  Сопровождение сайтов
                </p>
                <p @click="$emit('Portfolio')" class="footer-text">Портфолио</p>
                <p @click="$emit('StackTechnology')" class="footer-text">
                  Стек Технологий
                </p>
                <nuxt-link
                  to="/policy.pdf"
                  target="_blank"
                  class="logotype__policy-mobile"
                  >Политика Конфиденциальности</nuxt-link
                >
              </div>
            </div>
          </div>
        </div>
      </div> -->
    </div>
  </template>
  
  <style scoped>
  .footer-text {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 15px;
    line-height: 18px;
    color: #FFFFFF;
    cursor: pointer;
  }
  
  /*------------------FOOTER----------------*/
  .footer {
    background: #000000;
    width: 100%;
    margin-top: auto;
    padding: 35px 0 119px;
  }
  
  .footer a {
    text-decoration: none !important;
  }
  
  .footer__container {
    max-width: 1145px;
    width: 100%;
    /*margin: 0 auto;*/
    margin-right: 40.8854vw;
    margin-left: 20.2604vw;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-direction: row;
  }
  .footer__logo {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 100%;
  }
  .logotype__image {
    object-fit: cover;
  }
  /* .footer__navigation {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  .footer-navigation__links {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  .footer-navigation__links a {
    font-family: "Montserrat";
    font-style: normal;
    font-weight: 400;
    font-size: 15px;
    line-height: 22px;
    color: #ffffff;
    float: left;
    margin-top: 15px;
  }
  .footer-navigation__links a:last-of-type {
    text-decoration: underline !important;
  }
  .footer-navigation__links a:first-of-type {
    margin-top: 0px !important;
  }
  .footer-navigation__address {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding-top: 26px;
  }
  .footer-navigation__address a {
    display: flex;
    align-items: center;
    margin-top: 15px;
  }
  .footer-navigation__address img {
    width: 1.1em;
    height: 18px;
    margin-right: 15px;
  }
  .footer-navigation__address a:first-child {
    margin-top: 0px;
  }
  .footer-navigation__address img:last-of-type {
    margin-top: 0;
  }
  .address__text {
    margin-bottom: 0 !important;
    font-family: "Montserrat";
    font-style: normal;
    font-weight: 400;
    font-size: 15px;
    line-height: 22px;
    color: #ffffff;
  }
  .logotype__policy {
    font-family: "Montserrat";
    font-style: normal;
    font-weight: 400;
    font-size: 15px;
    line-height: 22px;
    color: #ffffff;
  } */
  
  /*-----------------------MOBILE--------------------------*/
  .footer-mobile {
    background: #000000;
    margin-top: auto;
    width: 100%;
    padding: 20px 0 37px;
    margin: auto;
    max-width: 100%;
  }
  
  .footer-mobile a {
    text-decoration: none !important;
  }
  
  .footer__container-mobile {
    max-width: 500px !important;
    width: 100%;
    display: flex;
    flex-direction: column;
    /*margin-left: 10.2604vw;
        margin-right: 10.2604vw;*/
    margin: 0 auto;
    padding: 0 15px 0 15px !important;
    /* align-items: center; */
  }
  .footer__logo-mobile {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 100%;
  }
  .download-app {
    margin-top: 30px;
  }
  .follow-us-block {
    margin-top: 28px;
  }
  .follow-us-links a:last-child {
    margin-left: 23px;
  }
  .footer__navigation-mobile {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin-top: 32px;
  }
  .footer-navigation__links-mobile {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    /* padding: 10px 10px; */
  }
  .footer-navigation__links-mobile a {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 13px;
    line-height: 16px;
    color: #CDCDCD;
  }
  /* .footer-navigation__links-mobile a:first-of-type {
    margin-top: 10px !important;
  } */
  .footer-navigation__address-mobile {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding-top: 26px;
  }
  .footer-navigation__address-mobile a {
    display: flex;
    align-items: center;
    margin-top: 15px;
  }
  .footer-navigation__address-mobile img {
    width: 1.1em;
    height: 18px;
    margin-right: 15px;
  }
  .footer-navigation__address-mobile img:last-of-type {
    margin-top: 0;
  }
  .ozo-direct {
    float: left;
    margin-top: 22px;
  }
  .ozo-direct-text {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 10px;
    line-height: 12px;
    color: #CDCDCD;
  }
  .line {
    margin-top: 22px;
  }
  .address__text-mobile {
    margin-bottom: 0 !important;
    font-family: "Montserrat";
    font-style: normal;
    font-weight: 400;
    font-size: 15px;
    line-height: 22px;
    color: #ffffff;
    margin-left: 12.5333vw;
  }
  .logotype__policy-mobile {
    font-family: "Montserrat";
    font-style: normal;
    font-weight: 400;
    font-size: 15px;
    line-height: 22px;
    color: #ffffff;
  }

  @media screen and (max-width: 1742px) {
    .footer {
      background: linear-gradient(88.1deg, #000000 1.57%, #404040 99.91%);
      margin-top: auto;
      width: 100%;
      padding: 24px 0 119px;
      margin: auto;
    }
    .footer a {
      text-decoration: none !important;
    }
  
    .footer__container {
      max-width: 1145px;
      width: 100%;
      margin: 0 auto;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 12px 41px;
    }
  }
  @media screen and (max-width: 1008px) {
    .footer {
      width: auto;
    }
  }
  @media screen and (max-width: 1067px) {
    .footer {
      width: auto;
    }
  }
  </style>
  
  <script>
  export default {
    name: "FooterMain",
  };
  </script>
  