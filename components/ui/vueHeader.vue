<template>
  <header class="header d-flex align-center justify-center">
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
</style>
