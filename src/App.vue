<template>
  <div class="app" ref="app-container">
    <div class="task">
      <h2>Welcome to my Hullabalook Technical Assessment</h2>
      <h3>I ran out of time, and I think the main thing I would do next is componentise (if thats a word) the code, since it should be component based and it would make the code more readable</h3>
    </div>

    <div class="filters">
      <h3>Filters</h3>
      <label>
        <input
          type="checkbox"
          v-model="showAvailableOnly"
          @change="filterProducts"
        />
        Show Available Only
      </label>

      <div class="brand-filters">
        <h4>Brand Filter</h4>
        <label v-for="brand in uniqueBrands" :key="brand">
          <input
            type="checkbox"
            v-model="selectedBrands"
            :value="brand"
            @change="filterProducts"
          />
          {{ brand }}
        </label>
      </div>
    </div>

    <div class="sort-dropdown">
      <label for="sort">Sort by:</label>
      <select id="sort" v-model="sortOption" @change="sortProducts">
        <option value="ascendingPrice">Price: Low to High</option>
        <option value="descendingPrice">Price: High to Low</option>
        <option value="relevance">Relevance</option>
      </select>
    </div>

    <div class="product-counter">
      <p>Total Products: {{ filteredProducts.length }}</p>
    </div>

    <div class="product-grid">
      <ProductGridItem
        v-for="(product, index) in sortedProducts"
        :key="index"
        :product="product"
      />
    </div>
  </div>
</template>

<script>
import ProductGridItem from './components/ProductGridItem.vue';
import products from './data/products.json';

export default {
  name: 'App',
  components: {
    ProductGridItem,
  },
  data() {
    return {
      products,
      showAvailableOnly: false,
      selectedBrands: [],
      sortOption: 'ascendingPrice',
    };
  },
  computed: {
    uniqueBrands() {
      return [...new Set(this.products.map((product) => product.brand))];
    },
    filteredProducts() {
      let filtered = this.products;
      if (this.showAvailableOnly) {
        filtered = filtered.filter((product) => product.isAvailable);
      }
      if (this.selectedBrands.length > 0) {
        filtered = filtered.filter((product) =>
          this.selectedBrands.includes(product.brand)
        );
      }
      return filtered;
    },
    sortedProducts() {
      let sorted = [...this.filteredProducts];
      switch (this.sortOption) {
        case 'ascendingPrice':
          sorted.sort((a, b) => a.price - b.price);
          break;
        case 'descendingPrice':
          sorted.sort((a, b) => b.price - a.price);
          break;
        case 'relevance':
          sorted.sort((a, b) => {
            if (a.isAvailable === b.isAvailable) {
              return a.rank - b.rank;
            }
            return a.isAvailable ? -1 : 1;
          });
          break;
        default:
          break;
      }
      return sorted;
    },
  },
  methods: {
    filterProducts() {
    },
    sortProducts() {

    },
  },
};
</script>

<style>

.sort-dropdown {
  margin-bottom: 20px;
}

.app {
  max-width: 100%;
  margin: 0 auto;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  color: #606569;
  width: 100%;
}

.link {
  color: #3a7f71;
}

.filters {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.brand-filters {
  margin-top: 10px;
}

.product-counter {
  text-align: center;
  margin-bottom: 20px;
}

.product-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.product-grid-item {
  background: #ddebe8;
  max-width: 200px;
  margin: 10px;
  padding: 10px;
}

.product-image {
  width: 100%;
}
</style>
