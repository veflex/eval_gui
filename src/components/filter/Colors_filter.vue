<template>
    <div class="colors_filter" id="colors_filter">
        <h2>Colors</h2>
        <div @click="emitColor($event)" class="carre" v-for="(color,i) in colors" :key="i" :style="{ background: color}"></div>
    </div>
</template>
<script>
export default {
  created() {
    //reset
    var that = this;
    this.$ebus.$on("reset", function() {
      const div = document.querySelector(".is-active");
      if (div) {
        that.$parent.$emit("colors-filter", "");
        div.classList.remove("is-active");
      } else return;
    });
  },
  props: ["colors"],
  methods: {
    handleActiveColor(evt) {
      var active = document.querySelector(".is-active");
      if (active === evt.target) {
        evt.target.classList.remove("is-active");
      } else if (active) {
        active.classList.remove("is-active");
        evt.target.classList.add("is-active");
      } else {
        evt.target.classList.add("is-active");
      }
    },
    emitColor(evt) {
      this.handleActiveColor(evt);
      this.$parent.$emit("colors-filter", evt.target.style["background"]);
    }
  }
};
</script>
<style lang="scss" scoped>
.colors_filter {
  // position: absolute;
  // top: 50%;
  // left: 10%;
  width: 200px;
  height: 200px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-items: center;
  h2 {
    text-align: left;
    width: 100%;
    margin: 0;
  }
}

.carre {
  width: 40px;
  height: 40px;
  border: 2px solid black;
}
.is-active {
  border: 2px solid yellowgreen;
}
</style>


