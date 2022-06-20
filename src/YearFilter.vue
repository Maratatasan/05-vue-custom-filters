<template>
  <div>Hello World</div>
</template>

<script setup>
const { params } = defineProps();

function updateFilter() {
  params.filterChangedCallback();
}

function isFilterActive() {
  return false;
}

function doesFilterPass() {
  return false;
}

function getModel() {
  return undefined;
}

function setModel() {}
</script>

<style lang="scss" scoped></style>
