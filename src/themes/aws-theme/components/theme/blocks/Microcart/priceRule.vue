<template>
  <div class="price-rule">
    <div v-if="differenceForFreeShipping > 0">
      Spend {{ differenceForFreeShipping.toFixed(2) }}$ more for free shipping
    </div>
    <div v-else>
      You spent enough for free shipping
    </div>
  </div>
</template>

<script>
import Microcart from '@vue-storefront/core/compatibility/components/blocks/Microcart/Microcart'

export default {
  mixins: [
    Microcart
  ],
  computed: {
    priceRuleValue () {
      return this.$store.getters['cart/getPriceRule']
    },
    subtotal () {
      let totalsArray = this.totals;
      let i

      for (i = 0; i < totalsArray.length; i++) {
        if (totalsArray[i].code === 'grand_total') {
          return totalsArray[i].value
        }
      }
    },
    differenceForFreeShipping () {
      return this.priceRuleValue - this.subtotal
    }
  }
};
</script>

<style lang="scss" scoped>
  .price-rule {
    background-color: lightgreen;
    font-family: 'Playfair Display', serif;
    padding: 20px 0;
    text-align: center;
    width: 100%;
  }
</style>
