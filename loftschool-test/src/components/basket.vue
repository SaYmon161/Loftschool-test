<template lang="pug">
  .basket
    statusbar(
      :checkedGoods="checkedGoods"
      @deleteChecked="deleteChecked"
      )
    ul.basket__list
      li.basket__item(v-for="(good, index) in goods")
        buy-item(
          :good="good"
          :index="index"
          @checkGood="checkGood"
          @reCalc="reCalc"
          :thousandSeparator="thousandSeparator"
          )
    .basket__subtotal
      .basket__subtotal-row 
        span.basket__subtotal-text Промежуточный итог по корзине:
        span.basket__subtotal-number {{thousandSeparator((this.sum).toFixed(2))}} Р
      .basket__subtotal-row
        span.basket__subtotal-text В том числе НДС:
        span.basket__subtotal-number {{thousandSeparator((this.sum * 0.18).toFixed(2))}} Р
    .basket__total
      .basket__total-row
        span.basket__total-text ИТОГО:
        span.basket__total-number  {{thousandSeparator((this.sum * 1.18).toFixed(2))}} Р
</template>

<script>
import buyItem from "./buyItem.vue";
import statusbar from "./statusbar.vue";

export default {
  components: {
    buyItem,
    statusbar
  },
  data() {
    return {
      goods: [],
      checkedGoods: [],
      sum: 0
    };
  },
  created() {
    this.goods = require("../data/goods.json");
    for (let item of this.goods) {
      this.sum += item.amount * item.price;
    }
  },
  methods: {
    checkGood() {
      this.checkedGoods = [...this.goods.filter(item => item.checked)];
    },
    deleteChecked() {
      for (let checkedGood of this.checkedGoods) {
        this.goods = this.goods.filter(item => {
          return item.id != checkedGood.id;
        });
      }
      this.checkedGoods = [];
      this.reCalc();
    },
    thousandSeparator(str) {
      var parts = (str + "").split("."),
        main = parts[0],
        len = main.length,
        output = "",
        i = len - 1;

      while (i >= 0) {
        output = main.charAt(i) + output;
        if ((len - i) % 3 === 0 && i > 0) {
          output = " " + output;
        }
        --i;
      }

      if (parts.length > 1) {
        output += "," + parts[1];
      }
      return output;
    },
    reCalc() {
      this.sum = 0;
      for (let item of this.goods) {
        this.sum += item.amount * item.price;
      }
    }
  }
};
</script>

<style lang="scss">
.basket__list {
  margin-bottom: 12px;
}

.basket__item {
  &:nth-child(even) {
    background-color: #f1f1f1;
  }
}

.basket__subtotal {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  margin-bottom: 20px;
  padding-top: 25px;
  padding-right: 20px;
  border-top: 1px solid #e5e5e5;
}

.basket__subtotal-number {
  display: inline-block;
  width: 130px;
  text-align: right;
  font-weight: bold;
  font-size: 18px;
}

.basket__subtotal-row {
  margin-bottom: 12px;

  &:last-child {
    margin-bottom: 0;
  }
}

.basket__total {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-right: 20px;
  color: #0a7eb5;

  &::before {
    content: "";
    display: block;
    width: 1045px;
    height: 3px;
    margin-bottom: 15px;
    background-image: linear-gradient(
      to right,
      black 29%,
      rgba(255, 255, 255, 0) 0%
    );
    background-position: top;
    background-size: 5px 1px;
    background-repeat: repeat-x;
  }
}

.basket__total-row {
  align-self: flex-end;
}

.basket__total-text {
  font-family: "pf_beausans_pro";
  font-weight: 400;
}

.basket__total-number {
  display: inline-block;
  width: 200px;
  text-align: right;
  font-weight: 700;
  font-size: 24px;
}
</style>
