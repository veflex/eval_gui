<template>
    <div class="product">
      <!-- <h2> Airmax</h2>
      <img src="../assets/img_products/air-force-black.jpg" alt="">     
      <p> 139€ </p> -->
      <h2 @click="test()"> {{ product.name }}</h2>
      <img :src="product.img" :alt="product.name">
      <p> {{ product.price }} € </p>
    </div>
</template>
<script>
export default {
  props: ["product"]
};
</script>
<style lang="scss" scoped>
.product {
  position: relative;
  width: 200px;
  height: 200px;
  border: 2px solid grey;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 7px 10px transparent;
  transition: all ease 0.3s;
  &:hover {
    box-shadow: 0 7px 10px rgba(0, 0, 0, 0.75);
  }
}
h2 {
  top: 10px;
  left: 10px;
  font-size: 1.7em;
  margin: 0;
  position: absolute;
}
img {
  display: block;
  min-width: 100%;
  width: 100%;
}
p {
  margin: 0;
  font-weight: bold;
  font-size: 1.5em;
  margin-top: 2%;
}
</style>
