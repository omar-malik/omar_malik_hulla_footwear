<template>
  <div class="sort-dropdown">
    <label for="sort">Sort by:</label>
    <select id="sort" v-model="selectedSortOption" @change="sortProducts">
      <option value="price-asc">Price: Low to High</option>
      <option value="price-desc">Price: High to Low</option>
      <option value="relevance">Relevance</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'SortBy',
  data() {
    return {
      selectedSortOption: 'price-asc',
    };
  },
  methods: {
    sortProducts() {
      this.$emit('input', this.selectedSortOption);
    },
  },
};
</script>

<style>

.sort-dropdown {
  margin-bottom: 20px;
}
</style>
