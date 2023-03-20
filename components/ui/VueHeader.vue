<template>
  <header class="header d-flex align-center justify-center">
    <!-- <vm-back-top :duration="250"></vm-back-top> -->
    <svg width="206" height="31" @click="$router.push('/')" class="header__icon">
      <use href="@/assets/icons/icons.svg#header-logo"></use>
    </svg>
  </header>
</template>

<script>
export default {
}
</script>


<style lang="scss" scoped>
.header {
  height: 60px;

  &__icon {
    cursor: pointer;
  }
}
// :deep(.vm-back-top-inner:hover) {
//   background-color: #E40613;
//   border-radius: 50%;
//   box-shadow: 0 1px 3px rgb(0 0 0 / 20%);
//   transition: all 0.2s ease-in-out;
//   width: 100%;
//   height: 100%;
// }
// :deep(.vm-back-top-inner) {
//   background-color: #E40613;
//   border-radius: 50%;
//   box-shadow: 0 1px 3px rgb(0 0 0 / 20%);
//   transition: all 0.2s ease-in-out;
//   width: 100%;
//   height: 100%;
// }
// :deep(.vm-back-top i) {
//   color: #fff;
//   font-size: 15px;
//   padding: 10px 15px;
//   /* border-radius: 50%; */
//   /* padding: 20px; */
// }
</style>
