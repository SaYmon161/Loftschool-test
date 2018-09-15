<template lang="pug">
  nav.menu
    ul.menu__list
      li.menu__item 
        a(href="#").menu__link каталог продукции
      li.menu__item
        a(href="#").menu__link все бренды
      li.menu__item
        a(href="#").menu__link подарки на 14 февраля
      li.menu__item
        a(href="#").menu__link подарки на 23 февраля
      li.menu__item
        a(href="#").menu__link подарки на 8 марта
</template>

<style lang="scss">
.menu {
  width: 100%;
  font-family: "pf_beausans_pro";
  font-weight: 300;
  font-size: 16px;
  text-transform: uppercase;
}

.menu__list {
  display: flex;
  width: 100%;
  height: 50px;
  background: linear-gradient(to bottom, #92c8e1, #b0d9ec);
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
}

.menu__item {
  flex-grow: 1;
  background: linear-gradient(to right, #92c8e1, #b0d9ec);
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  border-bottom-left-radius: 5px;

  &:first-child {
    border-bottom-left-radius: 0;
  }

  &:hover {
    margin: -1px -1px;
    border: 1px solid #cecece;
  }
}

.menu__link {
  display: flex;
  align-items: center;
  padding-left: 20px;
  width: 100%;
  height: 100%;

  &::after {
    content: "";
    display: block;
    margin-left: 9px;
    width: 5px;
    height: 5px;
    border-left: 1px solid #000;
    border-bottom: 1px solid #000;
    border-radius: 1px;
    transform: rotate(-45deg) translate(2px);
  }
}
</style>

