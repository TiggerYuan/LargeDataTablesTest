<template>
  <n-data-table
    :columns="columns"
    :data="data"
    :bordered="false"
    :max-height="500"
  />
</template>

<script lang="ts" setup>
import { h, ref, onMounted } from "vue";
import { NButton, useMessage, NDataTable } from "naive-ui";
import type { DataTableColumns } from "naive-ui";
import axios from "axios";

interface ITableData {
  id: number;
  name: string;
  index: number;
}
const data = ref<ITableData[]>();
// const message = useMessage();
const columns = ref([
  {
    title: "id",
    key: "id",
  },
  {
    title: "name",
    key: "name",
  },
  {
    title: "index",
    key: "no",
  },
  {
    title: "operations",
    key: "operations",
  },
  {
    title: "operations2",
    key: "operations2",
  },
]);
const init = () => {
  axios
    .get("/api/api/tables")
    .then((result) => {
      data.value = result.data as ITableData[];
    })
    .catch((err) => {});
};
onMounted(() => {
  init();
});
</script>
