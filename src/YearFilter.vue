<template>
  <div>
    <div class="filter-title">{{ params.title }}</div>
    <label
      v-for="(value, index) in filterOptions"
      :key="index"
    >
      <input
        type="radio"
        :value="value"
        v-model="filterState"
        @change="updateFilter()"
      />
      {{ value }}
    </label>
  </div>
</template>

<script setup>
import { ref } from "@vue/reactivity";

const { params } = defineProps();

const {field} = params.colDef

const filterState = ref("Filter off");
const filterOptions = ["Filter off", "2004", "2008"];

function updateFilter() {
  params.filterChangedCallback();
}

function isFilterActive() {
  return filterState.value != "Filter off";
}

function doesFilterPass(params) {
 
  return params.data[field] == filterState.value;
}

function getModel() {
  return undefined;
}

function setModel() {}
</script>

<style lang="scss" scoped></style>
