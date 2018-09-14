<template lang="pug">
  .popup-back(@click.self="popupClose")
    .popup(
      :style="{top: popupPosition.top + 'px', left:popupPosition.left + 'px'}"
      )
      h2.popup__title Изменить количество
      .popup__calculator
        .popup__price {{thousandSeparator(good.price)}}
        .popup__mul x
        .popup__amount
          .popup__amount-minus
          input(type="text" v-model="calcAmount").popup__amount-input
          .popup__amount-plus
        .popup__cost {{thousandSeparator(good.price * calcAmount)}} Р
      .popup__control
        a(href="#", title="сохранить" @click="saveAmount").popup__link.popup__link--blue сохранить
        a(href="#" title="отменить" @click="popupClose").popup__link отменить
</template>

<script>
export default {
  data() {
    return {
      calcAmount: 0
    };
  },
  props: {
    good: Object,
    popupPosition: Object,
    thousandSeparator: Function
  },
  created() {
    this.calcAmount = this.good.amount;
  },
  methods: {
    popupClose() {
      this.$emit("popupClose");
    },
    saveAmount() {
      this.good.amount = this.calcAmount;
      this.popupClose();
    }
  }
};
</script>


<style lang="scss">
.popup-back {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: hidden;
}

.popup {
  position: absolute;
  z-index: 100;
  transform: translate(-50%, -50%);
  width: 320px;
  height: 135px;
  padding: 20px 30px;
  border-radius: 5px;
  background: #fff;
  box-shadow: 0px 0px 20px 2px rgba(97, 97, 97, 1);
  -webkit-box-shadow: 0px 0px 20px 2px rgba(97, 97, 97, 1);
  -moz-box-shadow: 0px 0px 20px 2px rgba(97, 97, 97, 1);
}

.popup__title {
  margin-bottom: 20px;
  font-family: "pf_din_text_cond_pro";
  color: #05689b;
  font-weight: 500;
  font-size: 15px;
}
.popup__calculator {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.popup__amount {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 110px;
}

.popup__amount-minus {
  position: relative;
  width: 20px;
  height: 20px;
  background-color: #559abc;

  &:after {
    content: "";
    position: absolute;
    display: block;
    height: 2px;
    width: 10px;
    background-color: #fff;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
}

.popup__amount-plus {
  position: relative;
  width: 20px;
  height: 20px;
  background-color: #559abc;

  &:after {
    content: "";
    position: absolute;
    display: block;
    height: 2px;
    width: 10px;
    background-color: #fff;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }

  &:before {
    content: "";
    position: absolute;
    display: block;
    height: 2px;
    width: 10px;
    background-color: #fff;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) rotate(-90deg);
  }
}

.popup__amount-input {
  width: 50px;
  padding: 3px 8px;
  border: 1px solid #c0c0c0;
  border-radius: 3px;
  text-align: center;
  box-shadow: inset 0px 0px 0px 2px rgba(240, 240, 240, 1);
  -webkit-box-shadow: inset 0px 0px 0px 2px rgba(240, 240, 240, 1);
  -moz-box-shadow: inset 0px 0px 0px 2px rgba(240, 240, 240, 1);
}

.popup__price {
  width: 50px;
}

.popup__cost {
  display: flex;
  justify-content: flex-end;
  width: 80px;
}

.popup__link {
  font-size: 12px;
  text-transform: uppercase;
  text-decoration: underline;
  margin-right: 25px;
}

.popup__link--blue {
  color: #05689b;
}
</style>
