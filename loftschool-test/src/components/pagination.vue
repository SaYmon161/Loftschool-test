<template lang="pug">
  nav.pagination
    ul.pagination__list
      li.pagination__item
        a.pagination__link(href='#') Главная
      li.pagination__item Корзина
</template>

<style lang="scss">
.pagination {
  align-self: flex-start;
  margin-bottom: 10px;
}

.pagination__list {
  display: flex;
}

.pagination__item {
  display: flex;

  &::after {
    content: "/";
    display: block;
    margin-right: 9px;
    margin-left: 9px;
  }

  &:last-child:after {
    display: none;
  }
}

.pagination__link {
  text-decoration: underline;
}

.pagination__link--current {
  text-decoration: none;
}
</style>
