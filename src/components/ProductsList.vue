<template>  
    <div class="productsList">
        <product v-for="(product, i) in productsList" :key="i" :product="product"/>    
    </div>
</template>

<script>
import product from "@/components/Product.vue";

export default {
  components: {
    product
  },
  methods: {
    test(a) {
      console.log(a);
    }
  },
  props: ["productsList"]
};
</script>

<style>
.productsList {
  /* bottom: 10px;
  right: 10px;
  position: absolute; */
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  flex-wrap: wrap;
}
</style>


