<template>
  <div class="brand-filters">
    <h4>Brand Filter</h4>
    <label v-for="brand in brands" :key="brand">
      <input
        type="checkbox"
        v-model="selectedBrands"
        :value="brand"
        @change="filterProducts"
      />
      {{ brand }}
    </label>
  </div>
</template>

<script>
export default {
  name: 'BrandFilters',
  props: {
    brands: Array,
    value: Array,
  },
  computed: {
    selectedBrands: {
      get() {
        return this.value;
      },
      set(selectedBrands) {
        this.$emit('input', selectedBrands);
      },
    },
  },
  methods: {
    filterProducts() {
      this.$emit('input', this.selectedBrands);
    },
  },
};
</script>

<style>

.brand-filters {
  margin-top: 10px;
}
</style>
