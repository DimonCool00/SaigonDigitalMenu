<template>
  <footer class="footer d-flex flex-column align-center">
   <nuxt-link to="/">
     <svg width="206" height="31" class="footer__logo">
       <use href="@/assets/icons/icons.svg#footer-logo"></use>
     </svg>
   </nuxt-link>
   <div class="d-flex flex-column" style="margin-top: 26px;">
      <p class="footer-text text-tablet">Скачать мобильное приложение</p>
      <div class="footer__apps">
        <img src="@/assets/images/footer/appstore.png"/>
        <img src="@/assets/images/footer/gp.png" />
      </div>
    </div>
    <div class="f-flex flex-column">
      <p class="footer-text">Подписаться на нас</p>
      <div class="d-flex align-center icon-tablet">
        <a 
          href="https://www.facebook.com/coffeeonsaigon/" 
          target="_blank"
        >
          <img src="~/assets/facebook.svg">
        </a>
        <a 
          href="https://www.instagram.com/coffeeon_saigon/2"
          target="_blank" 
          style="margin-left: 23px;"
        >
          <img src="~/assets/instagram.svg">
        </a>
        <!-- <svg class="footer__socials" width="29" height="29">
          <use href="@/assets/icons/icons.svg#footer-insta"></use>
        </svg> -->
        </div>
    </div>
    <div class="footer__rules d-flex align-center justify-space-between">
      <a href="https://testapi.rst.ozo.direct/Doc/ConfidentialityPolicy.pdf" target="_blank">
        <span>Политика конфиденциальности</span>
      </a>
      <a>
        <span>Публичная оферта</span>
      </a>
    </div>
    <br />
    <blockquote class="footer__blockquote">
      OZO.DIRECT
    </blockquote>
  </footer>
</template>

<script>

</script>

<style lang="scss" scoped>
.footer {
  background: black;
  padding: 20px 15px 50px 15px;
  &-text {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 15px;
    line-height: 18px;
    color: #FFFFFF;
  }
  &__apps {
    margin-bottom: 26px;
    img {
      max-width: 147px;
      object-fit: cover;

      &:first-of-type {
        margin-right: 18px;
      }
    }
  }
  &__socials {
    margin-right: 23px;
    &:last-of-type {
      margin-right: 0;
    }
  }
  &__rules {
    margin-top: 38px;
    padding-bottom: 22px;
    border-bottom: 1px solid #CDCDCD;
    span {
      font-family: 'Inter';
      font-style: normal;
      font-weight: 400;
      font-size: 13px;
      line-height: 16px;
      color: #CDCDCD;
    }
    a {
      text-decoration: none;
    }
  }
  blockquote {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 10px;
    line-height: 12px;
    color: #CDCDCD;
  }
}
p, div {
  color:#FFFFFF;
}
@media screen and (max-width: 600px) {
  .footer {
    align-items: unset !important;
  }
}

@media screen and (min-width: 600px) {
  .footer {
    &-text{
      align-items: unset !important;
    }
  }
  .footer__rules span:first-child {
    padding-left: 0px !important;
  }
  .footer__rules a:last-child {
    padding-left: 30px;
  }
  .text-tablet {
    text-align: center !important;
  }
.icon-tablet {
  justify-content: space-evenly;
}
.icon-tablet a:last-child {
  margin-left: 0px !important;
}
}
</style>
