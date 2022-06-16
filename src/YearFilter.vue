<template>
  <div>
  <div class="filter-title">My Year Filter</div>
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

<script>
import { reactive, ref } from "@vue/reactivity";

export default {
  setup(props) {
    const { params } = props;
    let year = ref( "All" );

    function updateFilter(newValue) {
      year.value = newValue
      params.filterChangedCallback();
    }

    function doesFilterPass({ data }) {
      return data.year >= 2010;
    }

    function isFilterActive() {
      return year.value === "2010";
    }

    function getModel() {}

    function setModel() {}

    return {
      updateFilter,
      doesFilterPass,
      isFilterActive,
      getModel,
      setModel,
      year,
    };
  },
};
</script>

<style lang="scss" scoped></style>
