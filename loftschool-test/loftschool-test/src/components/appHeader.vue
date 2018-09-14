<template lang="pug">
  header.header
    .header__row.header__row--top
      .logo
        img.logo__img(src='../assets/images/logo.png')
      search
    .header__row
      app-menu
</template>

<script>
import search from "./search.vue";
import appMenu from "./appMenu.vue";

export default {
  components: {
    search,
    appMenu
  }
};
</script>

<style lang="scss">
.header {
  display: flex;
  flex-direction: column;
  width: 100%;
  margin-bottom: 54px;
}

.header__row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  margin-bottom: 40px;

  &:last-child {
    margin-bottom: 0;
  }
}

.header__row--top {
  padding-left: 12px;
}

.logo__img {
  width: 217px;
  height: 57px;
}
</style>
