<template>
    <button class="reset" @click="reset">Reset filter</button>
</template>
<script>
export default {
  methods: {
    reset() {
      this.$ebus.$emit("reset");
    }
  }
};
</script>
<style>
.reset {
  /* position: absolute;
  top: 5%;
  left: 10%; */
  width: 100px;
}
</style>
