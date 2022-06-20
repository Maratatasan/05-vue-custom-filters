<template>
  <div class="my-filter">
    <div>Hello World</div>
    <label>
      <input
        type="radio"
        name="my-year-filter"
        @change="updateFilter('All')"
      />
      All
    </label>
    <label>
      <input
        type="radio"
        name="my-year-filter"
        @change="updateFilter('2010')"
      />
      Since 2010
    </label>
  </div>
</template>

<script setup>
import { ref } from "@vue/reactivity";

const { params } = defineProps({ params: {} });

let year = ref("All");
function updateFilter(newValue) {
  year.value = newValue;
  params.filterChangedCallback();
}
function doesFilterPass({ data }) {
  return data.year >= 2010;
}
function isFilterActive() {
  return year.value !== "All";
}

function getModel() {
  return undefined;
}
function setModel() {}
</script>

<style lang="scss" scoped></style>
