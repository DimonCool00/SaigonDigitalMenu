
<template>
    <div class="header-container">
      <vm-back-top :duration="250"></vm-back-top>
        <div class="header-content">
            <div class="header-logo">
                <nuxt-link to="/">
                <img src="~/assets/header_logo.svg" alt="" />
                </nuxt-link>
            </div>
            <div class="search-container">
                <img src="~/assets/Group 7600.png" alt="search icon" class="search-icon">
                <input type="text" placeholder="Поиск" class="search-input">
            </div>
        </div>
            <div class="menu-wrapper sticky-element menu" v-scroll="stickyElement">
                <v-scroll>
                    <ul class="menu-items" >
                        <li v-for="(item, index) in menuItems" :key="item.id">
                            <a :ref="`menuitem-${item.textNum}`" :href="`#menuitem-${item.textNum}`" :class="`menunav-${index}`">{{ item.text }}</a>
                        </li>
                    </ul>
                </v-scroll>
            </div>  
    </div>
</template>


<style scoped>
.sticky {
  position: fixed;
  top: 0;
  width: 100%;
  padding: 10px;
  height: 50px;
  background: #FFFFFF;
  scroll-margin-top: 100px;
  margin-bottom: 20px;
}
.category-padding {
  padding-top: 45px;
}
.header-content {
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  /* margin-top: 60px; */
  margin-bottom: 18px;
}
.header-container {
    /* position: relative; */
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    margin-top: 15px;
    margin-left: auto;
    margin-right: auto;
    background-color: #FFFFFF;
    color: black;
    margin-bottom: 18px;
}
.search-container {
  display: flex;
  align-items: center;
  border-radius: 8px;
  padding: 8px 5px;
  background-color: #F0F1F3;
  width: 100%;
  min-width: 360px;
}

.search-icon {
  width: 15px;
  height: 15px;
  margin-right: 13px;
  margin-left: 8px;
}

.search-input {
  flex: 1;
  border: none;
  outline: none;
  font-size: 18px;
}
.menu-wrapper {
  width: 100%; /* задаем фиксированную ширину */
  /* overflow-x: auto; */
  overflow-x: scroll; /* добавляем горизонтальную прокрутку при необходимости */
  list-style: none;
  white-space: nowrap;
  box-shadow: 0px 3px 4px rgba(137, 113, 113, 0.09);
  height: 45px;
  /* position: fixed;
  top: 40;
  left: 0;
  right: 0; */
}
.menu-wrapper::-webkit-scrollbar {
  height: 0px;
  background-color: #ffffff;
}

.menu-wrapper::-webkit-scrollbar-thumb {
  background-color: rgb(255, 250, 250);
}

.menu-items  {
  display: flex;
  flex-wrap: nowrap; /* запрещаем перенос элементов на новую строку */
  list-style-type: none;
  justify-content: space-between;
  height: 35px;
}
.menu-items ul a{
    list-style-type: none;
}
.menu-items a {
    text-decoration: none;
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 19px;
    color: #000;
    padding: 15px;
    width: 100%;
}
.menu-items li:hover {
    background: #5E5E5E;
    border-radius: 5px;
    color: #fff;
    padding: 3px;
}
.menu-items a:active {
    color: #fff;
}
.menu-items a:hover {
    color: #fff;
}  
.menu-items li:active {
    background: #5E5E5E;
    border-radius: 5px;
    color: #fff;
}
.menu-items a:first-child {
    padding-left: 10px;
}
/* a.menunav-0 {
    padding-left: 10px;
    font-weight: 600;
    font-size: 16px;
    line-height: 19px;
    color: #000;
} */
:deep(.vm-back-top-inner:hover) {
  background-color: #E40613;
  border-radius: 50%;
  box-shadow: 0 1px 3px rgb(0 0 0 / 20%);
  transition: all 0.2s ease-in-out;
  width: 100%;
  height: 100%;
}
:deep(.vm-back-top-inner) {
  background-color: #E40613;
  border-radius: 50%;
  box-shadow: 0 1px 3px rgb(0 0 0 / 20%);
  transition: all 0.2s ease-in-out;
  width: 100%;
  height: 100%;
}
:deep(.vm-back-top i) {
  color: #fff;
  font-size: 15px;
  padding: 10px 15px;
  /* border-radius: 50%; */
  /* padding: 20px; */
}
</style>

<script>

import VScroll from 'vue-scrollview';

export default {
    name: 'HeaderMain',
    props: {
  },
  data() {
    return {
        drawer: false,
        group: null,
        menuItems: [
        { id: 1, text: 'Завтраки', textNum: '5', link: '/' },
        { id: 2, text: 'Салаты и закуски', textNum: '10', link: '/about' },
        { id: 3, text: 'Супы', textNum: '21', link: '/services' },
        { id: 4, text: 'Мясо и Тофу', link: '/products' },
        { id: 5, text: 'Морепродукты и рыба', link: '/contacts' },
        { id: 6, text: 'Лапша и рис', link: '/sitemap' },
        { id: 7, text: 'Суши', link: '/blog' },
        { id: 8, text: 'Гарниры', link: '/faq' },
        { id: 9, text: 'Десерты', link: '/terms' },
        { id: 10, text: 'Хлеб', link: '/privacy' },
        { id: 11, text: 'Безалкогольные напитки', link: '/privacy' },
        { id: 12, text: 'Бутылочное пиво', link: '/privacy' },
        { id: 13, text: 'Закуски к пиву', link: '/privacy' }
      ],
      searchQuery: '',
    }
  },
  watch: {
    // searchText() {
    //   this.$emit('input', this.searchText);
    // },
    },
  methods: {
    stickyElement() {
      const stickyEl = document.querySelector('.sticky-element');
      const scrollTop = window.pageYOffset;

      if (scrollTop > 120) {
        stickyEl.classList.add('sticky');
      } else {
        stickyEl.classList.remove('sticky');
      }
    }
  }
};

</script> 