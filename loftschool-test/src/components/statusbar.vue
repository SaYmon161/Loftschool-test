<template lang="pug">
  .statusbar
    .statusbar__left
      span.statusbar__left-text Выделено
      span.statusbar__left-counter {{checkedGoods.length}}
    .statusbar__right
      a(href="#" @click.prevent="deleteChecked").statusbar__delete-link
        .statusbar__delete-icon
        .statusbar__delete-text Удалить отмеченные
</template>

<script>
export default {
  props: {
    checkedGoods: Array
  },
  methods: {
    deleteChecked() {
      this.$emit("deleteChecked");
    }
  }
};
</script>


<style lang="scss">
.statusbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 43px;
  padding: 0 17px;
  background-color: #d9e8ef;
  font-family: "pf_beausans_probbook";
}

.statusbar__left-text {
  margin-right: 5px;
}

.statusbar__left-counter {
  font-family: "pf_beausans_pro";
  font-weight: 600;
}

.statusbar__delete-link {
  display: flex;
  align-items: center;
}

.statusbar__delete-icon {
  position: relative;
  width: 20px;
  height: 20px;
  margin-right: 10px;
  background-color: #7f7f7f;
  border-radius: 3px;

  &::after {
    content: "";
    display: block;
    position: absolute;
    height: 3px;
    width: 10px;
    background-color: #d9e8ef;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) rotate(-45deg);
  }

  &::before {
    content: "";
    display: block;
    position: absolute;
    height: 3px;
    width: 10px;
    background-color: #d9e8ef;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) rotate(45deg);
  }
}

.statusbar__delete-text {
  text-decoration: underline;
}
</style>

