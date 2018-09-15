<template lang="pug">
  .buy-item
    .buy-item__check-col.buy-item__col
      label.buy-item__label
        input.buy-item__checkbox(type="checkbox" v-model="good.checked" @change="checkGood")
        .buy-item__custom-checkbox
      span.buy-item__order {{index + 1}}
    .buy-item__img-col.buy-item__col
      img(:src="getImgUrl(good.image)").buy-item-item__img
    .buy-item__name-col.buy-item__col {{good.name}}
    .buy-item__price-col.buy-item__col
      span.buy-item__price {{thousandSeparator(good.price)}} Р
      span.buy-item__mul x
      input(
        type="text"
        v-model="good.amount"
        @click="openPopup"
        readonly
        :id="good.id"
        ).buy-item__amount-input
      span.buy-item__equal =
      span.buy-item__cost {{thousandSeparator(cost)}} Р
    popup(
      v-if="popupOpen"
      :good="good"
      @popupClose="popupClose"
      :popupPosition="popupPosition"
      :thousandSeparator="thousandSeparator"
      )
</template>

<script>
import popup from "./popup.vue";

export default {
  components: {
    popup
  },
  data() {
    return {
      popupOpen: false,
      popupPosition: {}
    };
  },
  props: {
    good: Object,
    index: Number,
    thousandSeparator: Function
  },
  created() {
    this.good.checked = false;
  },
  methods: {
    openPopup() {
      let amountInput = document.getElementById(`${this.good.id}`);
      this.popupPosition.top = amountInput.getBoundingClientRect().top;
      this.popupPosition.left = amountInput.getBoundingClientRect().left;
      this.popupOpen = true;
    },
    popupClose() {
      this.popupOpen = false;
    },
    getImgUrl(img) {
      let images = require.context(
        "../assets/images",
        false,
        /\.(png|jpe?g|gif|webp)(\?.*)?$/
      );
      return images("./" + img);
    },
    checkGood() {
      this.$emit("checkGood");
    }
  },
  computed: {
    cost() {
      return this.good.price * this.good.amount;
    }
  },
  watch: {
    cost() {
      this.$emit("reCalc");
    }
  }
};
</script>


<style lang="scss">
.buy-item {
  display: flex;
  align-items: center;
  height: 75px;
}

.buy-item__col {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  background-image: linear-gradient(black 29%, rgba(255, 255, 255, 0) 0%);
  background-position: right;
  background-size: 1px 5px;
  background-repeat: repeat-y;

  &:last-child {
    background: none;
  }
}

.buy-item__check-col {
  width: 86px;
}

.buy-item__label {
  display: flex;
  margin-right: 23px;
}

.buy-item__custom-checkbox {
  position: relative;
  width: 20px;
  height: 20px;
  background-color: #fff;
  border: 1px solid #d7d7d7;
  border-radius: 3px;
  box-shadow: inset 0px 0px 0px 2px rgba(240, 240, 240, 1);
  -webkit-box-shadow: inset 0px 0px 0px 2px rgba(240, 240, 240, 1);
  -moz-box-shadow: inset 0px 0px 0px 2px rgba(240, 240, 240, 1);

  &::after {
    content: "";
    display: none;
    position: absolute;
    background: url(../assets/images/check.png);
    width: 14px;
    height: 12px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
}

.buy-item__checkbox {
  position: absolute;
  left: -99999px;

  &:checked + .buy-item__custom-checkbox::after {
    display: block;
  }
}

.buy-item__img-col {
  width: 95px;
}

.buy-item__name-col {
  justify-content: flex-start;
  width: 627px;
  padding-left: 27px;
  padding-right: 105px;
}

.buy-item__price-col {
  width: 300px;
  padding: 0 22px;
  display: flex;
  justify-content: space-between;
}

.buy-item__amount-input {
  width: 50px;
  padding: 3px 6px;
  border: 1px solid #c0c0c0;
  border-radius: 3px;
  text-align: center;
  box-shadow: inset 0px 0px 0px 2px rgba(240, 240, 240, 1);
  -webkit-box-shadow: inset 0px 0px 0px 2px rgba(240, 240, 240, 1);
  -moz-box-shadow: inset 0px 0px 0px 2px rgba(240, 240, 240, 1);
}

.buy-item__price {
  width: 70px;
}

.buy-item__cost {
  display: flex;
  justify-content: flex-end;
  width: 80px;
}
</style>
