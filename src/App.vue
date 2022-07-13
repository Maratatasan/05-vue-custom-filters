<template>
  <button @click="onBtnSave()">Save</button>
  <button @click="onBtnRestore()">Restore</button>
  <button @click="onBtnCustomApi()">Custom Api</button>
  <ag-grid-vue
    style="width: 100%; height: 95vh"
    class="ag-theme-alpine"
    :rowData="rowData.rows"
    :columnDefs="columnDefs.columns"
    :defaultColDef="defaultColDef.def"
    @grid-ready="onGridReady"
  >
  </ag-grid-vue>
</template>

<script>
import { AgGridVue } from "ag-grid-vue3";

import { reactive, h, onMounted, ref } from "vue";
import MyFilter from "./YearFilter.vue";

export default {
  name: "App",
  components: {
    AgGridVue,
    YearFilterVue: MyFilter,
  },
  setup(props) {
    const gridApi = ref(null);
    let savedFilterState;

function onBtnCustomApi(){
  gridApi.value.getFilterInstance('year', instance =>{
    instance.myCustomFilterMethod()
  })
}

    function onGridReady(params) {
      gridApi.value = params.api;
    }
    function onBtnSave() {
      const model = gridApi.value.getFilterModel();
      console.log("saving", model);
      savedFilterState = model;
    }
    function onBtnRestore() {
      gridApi.value.setFilterModel(savedFilterState);
    }
    const rowData = reactive({
      rows: [],
    });
    const columnDefs = reactive({
      columns: [
        { field: "athlete", filter: true },
        {
          field: "year",
          filter: MyFilter,
          floatingFilter: true,
          filterParams: {
            title: "Year Filter",
            values: [2000, 2006, 2008],
          },
        },
        {
          field: "age",
          filter: MyFilter,
          floatingFilter: true,
          filterParams: {
            title: "Age Filter",
            values: [18, 19, 20, 21],
          },
        },
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

    return {
      columnDefs,
      rowData,
      defaultColDef,
      onGridReady,
      onBtnSave,
      onBtnRestore,
      onBtnCustomApi
    };
  },
};
</script>

<style lang="scss">
@import "~ag-grid-community/dist/styles/ag-grid.css";
@import "~ag-grid-community/dist/styles/ag-theme-alpine.css";
</style>
