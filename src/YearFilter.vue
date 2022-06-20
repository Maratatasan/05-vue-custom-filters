<template>
  <div>Hello World</div>
</template>

<script>
export default {
  setup(props) {
    const { params } = props;
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
    return {
      updateFilter,
      doesFilterPass,
      isFilterActive,
      getModel,
      setModel,
    };
  },
};
</script>

<style lang="scss" scoped></style>
