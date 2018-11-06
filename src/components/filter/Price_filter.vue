<template>
    <div class="price_filter">
        <label for="price_filter">Price Max: {{price_filter}}</label>
        <input type="range" id="price_filter" v-model="price_filter" name="price_filter" :min="range.min" :max="range.max" step="1" @input="emitPrice"  />
    </div>    
</template>

<script>
export default {
  //reset
  created() {
    var that = this;
    this.$ebus.$on("reset", function() {
      that.price_filter = null;
      that.$parent.$emit("price-filter", that.price_filter);
    });
  },
  methods: {
    emitPrice() {
      this.$parent.$emit("price-filter", this.price_filter);
    }
  },
  props: ["range"],
  data() {
    return {
      price_filter: 0
    };
  }
};
</script>

<style lang="scss" scoped>
.price_filter {
  // position: absolute;
  // top: 10%;
  // left: 10%;
  width: 100%;
  text-align: left;
}
</style>


