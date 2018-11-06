<template>
  <div class="eval">
    <aside class="aside">
      <reset/>
      <pricefilter :range="range"/>
      <brandsfilter :brands="brands"/>
      <colorsfilter :colors="colors"/>
    </aside>    
    <productsList class="productList" :productsList="products"/>

  </div>
</template>

<script>
// @ is an alias to /src
import productsList from "@/components/ProductsList.vue";
import pricefilter from "@/components/filter/Price_filter.vue";
import brandsfilter from "@/components/filter/Brands_filter.vue";
import colorsfilter from "@/components/filter/Colors_filter.vue";
import reset from "@/components/filter/Reset.vue";
export default {
  created() {
    //on conserve le tableau avec tout les produit dedans
    this.fullProducts = this.products;
    //event handler
    this.eventHandler();
    //on récupère les marques de chaque produits en un seul exemplaire
    this.getBrands();
    //on envois la fourchette pour l'input range
    this.sendRange();
    //on récupère les colors
    this.getColors();
  },
  methods: {
    eventHandler() {
      var objectFilter = { price: null, brands: [], color: "" };
      //event sur input du range
      this.$on("price-filter", function(price) {
        objectFilter.price = price;
        this.filterHandler(objectFilter);
      });
      //event sur input des checkbox
      this.$on("brands-filter", function(brand) {
        if (brand === "") {
          objectFilter.brands = [];
        } else {
          var brandIndex = objectFilter.brands.indexOf(brand);
          if (brandIndex === -1) {
            objectFilter.brands.push(brand);
          } else {
            objectFilter.brands.splice(brandIndex, 1);
          }
        }

        this.filterHandler(objectFilter);
      });

      //event au click d'une couleur
      this.$on("colors-filter", function(color) {
        if (objectFilter.color === color) {
          objectFilter.color = "";
        } else {
          objectFilter.color = color;
        }
        this.filterHandler(objectFilter);
      });
      this.$on("reset", function(reset) {
        this.objectFilter = reset;
        this.filterHandler(objectFilter);
      });
    },
    //fonction gerant l'affichage par rapport au filtre donné
    filterHandler(filter) {
      this.products = this.fullProducts.filter(function(product) {
        if (
          (!filter.price || product.price <= filter.price) &&
          (!filter.brands.length || filter.brands.includes(product.brand)) &&
          (!filter.color || filter.color === product.color)
        ) {
          return true;
        }
      });
    },
    //fonction qui permet de récup un seul exemplaire d'élements dans un array
    onlyOne(array, param) {
      if (array.includes(param)) {
        return;
      } else {
        array.push(param);
      }
    },
    //on récup les marque en 1 seul exemplaire
    getBrands() {
      this.fullProducts.forEach(product => {
        this.onlyOne(this.brands, product.brand);
      });
    },
    //on récup les colors en un seul exemplaire
    getColors() {
      this.fullProducts.forEach(product => {
        this.onlyOne(this.colors, product.color);
      });
    },
    //récupère les prix et les classe en ordre croissant
    getPrices() {
      this.fullProducts.forEach(product => {
        this.prices.push(product.price);
      });
      this.prices.sort((a, b) => a - b);
    },
    getRange(array) {
      return { min: array[0], max: array[array.length - 1] };
    },
    sendRange() {
      this.getPrices();
      this.range = this.getRange(this.prices);
    }
  },
  name: "eval",
  data() {
    return {
      prices: [],
      brands: [],
      colors: [],
      range: {},
      products: [
        {
          name: "Air force",
          img: require("../assets/img_products/air-force-black.jpg"),
          price: 139,
          brand: "nike",
          color: "black"
        },
        {
          name: "Air force",
          img: require("../assets/img_products/air-force-white.jpg"),
          price: 139,
          brand: "nike",
          color: "white"
        },
        {
          name: "Airmax",
          img: require("../assets/img_products/air-max-bone.jpg"),
          price: 159,
          brand: "nike",
          color: "rgb(162, 153, 138)"
        },
        {
          name: "Asics",
          img: require("../assets/img_products/asics-pink.jpg"),
          price: 189,
          brand: "asics",
          color: "rgb(250, 57, 138)"
        },
        {
          name: "Jordan",
          img: require("../assets/img_products/jordan-black.jpg"),
          price: 99,
          brand: "jordan",
          color: "black"
        },
        {
          name: "NewBalance",
          img: require("../assets/img_products/newbalance-purple.jpg"),
          price: 79,
          brand: "new-balance",
          color: "rgb(70, 58, 96)"
        },
        {
          name: "Reebok",
          img: require("../assets/img_products/reebok-gold.jpg"),
          price: 99,
          brand: "reebok",
          color: "rgb(230, 192, 119)"
        },
        {
          name: "Vans",
          img: require("../assets/img_products/vans-mickey.jpg"),
          price: 399,
          brand: "vans",
          color: "white"
        },
        {
          name: "Vans",
          img: require("../assets/img_products/vans-red.jpg"),
          price: 69,
          brand: "vans",
          color: "rgb(180, 34, 44)"
        }
      ]
    };
  },
  components: {
    productsList,
    pricefilter,
    brandsfilter,
    colorsfilter,
    reset
  }
};
</script>
<style lang="scss" scoped>
.eval {
  display: flex;
  height: 90vh;
  justify-content: space-around;
  align-items: center;
  background: rgb(233, 232, 232);
}
.aside {
  width: 13%;
  height: 100%;
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
.productList {
  width: 50%;
}
</style>

