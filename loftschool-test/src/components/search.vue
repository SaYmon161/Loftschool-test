<template lang="pug">
  .search
    form.search__form(method="GET" )
      input.search__input(name="search" type="text")
      button.search__btn(type="submit") Поиск
</template>

<style lang="scss">
.search {
  padding-top: 20px;
}

.search__form {
  display: flex;
  align-items: center;
}

.search__input {
  margin-right: 8px;
  padding-left: 30px;
  width: 313px;
  height: 28px;
  border: 1px solid #d5d5d5;
  border-radius: 3px;
  outline: none;
  box-shadow: inset 0px 0px 0px 2px rgba(240, 240, 240, 1);
  -webkit-box-shadow: inset 0px 0px 0px 2px rgba(240, 240, 240, 1);
  -moz-box-shadow: inset 0px 0px 0px 2px rgba(240, 240, 240, 1);
  background: url("../assets/images/search.png") 10px center no-repeat;
}

.search__btn {
  width: 68px;
  height: 28px;
  border: none;
  border-radius: 2px;
  color: #ffffff;
  background-color: #17709a;
  font-size: 12px;
  text-transform: uppercase;

  &:hover {
    background-color: #1d97cf;
  }

  &:active {
    background-color: #10506e;
  }
}
</style>
