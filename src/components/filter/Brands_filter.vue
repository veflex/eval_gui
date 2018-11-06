<template>
    <div class="brands-filter">
        <h2>Brands</h2>
        <div v-for="(brand, i) in brands" :key="i">
            <label for=""> {{ brand }}  </label>
            <input @input='emitBrandName($event)'  :name="brand"  type="checkbox">
        </div>
        
    </div>
</template>
<script>
export default {
  created() {
    var that = this;
    this.$ebus.$on("reset", function() {
      const check = document.querySelectorAll("input");
      if (check) {
        check.forEach(checkbox => {
          checkbox.checked = false;
        });
        that.$parent.$emit("brands-filter", "");
      }
    });
  },
  methods: {
    emitBrandName(evt) {
      this.$parent.$emit("brands-filter", evt.target.name);
    }
  },
  props: ["brands"]
};
</script>

<style lang="scss" scoped>
.brands-filter {
  // position: absolute;
  // top: 20%;
  // left: 10%;
  text-align: left;
  width: 100%;
  div {
    position: relative;
    input {
      position: absolute;
      right: 10px;
    }
  }
}
</style>
