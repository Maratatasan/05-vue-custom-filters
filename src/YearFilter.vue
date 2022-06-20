<template>
  <div>
    <div class="filter-title">Year Filter</div>
    <label
      v-for="(value, index) in ['Filter off', 'Filter on']"
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

const filterState = ref("Filter off");

function updateFilter() {
  params.filterChangedCallback();
}

function isFilterActive() {
  return false;
}

function doesFilterPass(params) {
  return false;
}

function getModel() {
  return undefined;
}

function setModel() {}
</script>

<style lang="scss" scoped></style>
