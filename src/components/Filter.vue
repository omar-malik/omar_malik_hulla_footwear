<template>
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

    <BrandFilters
      :brands="uniqueBrands"
      v-model="selectedBrands"
      @input="filterProducts"
    />
  </div>
</template>

<script>
import BrandFilters from './BrandFilter.vue';

export default {
  name: 'Filters',
  components: {
    BrandFilters,
  },
  props: {
    products: Array,
  },
  data() {
    return {
      showAvailableOnly: false,
      selectedBrands: [],
    };
  },
  computed: {
    uniqueBrands() {
      return [...new Set(this.products.map((product) => product.brand))];
    },
  },
  methods: {
    filterProducts() {
      this.$emit('input', {
        showAvailableOnly: this.showAvailableOnly,
        selectedBrands: this.selectedBrands,
      });
    },
  },
};
</script>

<style>

.filters {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.brand-filters {
  margin-top: 10px;
}
</style>
