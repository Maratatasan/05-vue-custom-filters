<template>
  <div style="display: flex; flex-direction: column">
    <div class="filter-title">{{ params.title }}</div>
    <div>Filter State = {{ filterState }}</div>
    <button @click="updateFilter('Filter off')">
      Filter off
    </button>
    <button
      v-for="(value, index) in params.values"
      :key="index"
      @click="updateFilter(value)"
    >
      {{ value }}
    </button>
  </div>
</template>

<script setup>
import { ref } from "@vue/reactivity";

const { params } = defineProps();

const { field } = params.colDef;

const filterState = ref("Filter off");

function updateFilter(value) {
  filterState.value = value;
  params.filterChangedCallback();
}

function isFilterActive() {
  return filterState.value != "Filter off";
}

function doesFilterPass(params) {
  return params.data[field] == filterState.value;
}

function getModel() {
  if (filterState.value == "Filter off") {
    return undefined;
  }
  return { state: filterState.value };
}

function setModel(model) {
  if (model == null) {
    updateFilter("Filter off");
  } else {
    updateFilter(model.state);
  }
}
</script>

<style lang="scss" scoped></style>
