<template lang="pug">
  .wrapper
    .container
      app-header
      pagination
      main.maincontent
        h1.maincontent__title корзина
        basket
</template>


<script>
import appHeader from "./components/appHeader.vue";
import pagination from "./components/pagination.vue";
import basket from "./components/basket.vue";

export default {
  name: "app",
  components: {
    appHeader,
    pagination,
    basket
  }
};
</script>

<style  lang="scss">
@import "~normalize.css";

@import "./assets/styles/base.scss";
@import "./assets/styles/fonts.css";

.wrapper {
  display: flex;
  justify-content: center;
  height: 100%;
  width: 100%;
  overflow: hidden;
  padding-top: 32px;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 1110px;
}

.maincontent {
  width: 100%;
}

.maincontent__title {
  font-size: 30px;
  text-transform: uppercase;
  color: #0a7eb5;
  margin-bottom: 14px;
}
</style>
