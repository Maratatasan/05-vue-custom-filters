<template>
  <ag-grid-vue
    style="width: 100%; height: 95vh"
    class="ag-theme-alpine"
    :rowData="rowData.rows"
    :columnDefs="columnDefs.columns"
    :defaultColDef="defaultColDef.def"
  >
  </ag-grid-vue>
</template>

<script>
import { AgGridVue } from "ag-grid-vue3";

import { reactive, h, onMounted } from "vue";
import YearFilterVue from "./YearFilter.vue";

export default {
  name: "App",
  components: {
    AgGridVue,
    YearFilterVue,
  },
  setup(props) {
    const rowData = reactive({
      rows: [],
    });
    const columnDefs = reactive({
      columns: [
        { field: "athlete" },
        {
          field: "year",
          filter: YearFilterVue,
          filterParams: { title: "My custom filter" },
        },
        { field: "age" },
        { field: "country" },
      ],
    });

    const defaultColDef = reactive({
      def: { flex: 1 },
    });
    onMounted(() => {
      fetch(
        "https://www.ag-grid.com/example-assets/olympic-winners.json"
      )
        .then((resp) => resp.json())
        .then((data) => (rowData.rows = data));
    });

    return { columnDefs, rowData, defaultColDef };
  },
};
</script>

<style lang="scss">
@import "~ag-grid-community/dist/styles/ag-grid.css";
@import "~ag-grid-community/dist/styles/ag-theme-alpine.css";
</style>
