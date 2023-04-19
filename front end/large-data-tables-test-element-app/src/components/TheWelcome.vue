<script setup lang="ts">
import {
  ElButton,
  ElIcon,
  ElTag,
  ElTooltip,
  TableV2FixedDir,
  ElInput,
} from "element-plus";
import axios from "axios";
import { h, onMounted, ref } from "vue";
interface ITableData {
  id: number;
  name: string;
  index: number;
}
const columns = [
  {
    key: `id`,
    dataKey: `id`,
    title: `id`,
    width: 150,
  },
  {
    key: `name`,
    dataKey: `name`,
    title: `name`,
    width: 150,
  },
  {
    key: `index`,
    dataKey: `index`,
    title: `index`,
    width: 150,
  },
  {
    key: "operations",
    title: "Operations",
    cellRenderer: ({ rowData }: { rowData: ITableData }) =>
      h(
        ElButton,
        {
          size: "small",
          onClick: () => {
            rowData.index++;
            console.log(rowData);

            console.log(123);
          },
        },
        {
          default: () => "Edit",
        }
      ),
    width: 150,
    align: "center",
  },
  {
    key: "operations2",
    title: "Operations2",
    cellRenderer: ({ rowData }: { rowData: ITableData }) =>
      h(
        ElInput,
        {
          size: "small",
          modelValue: rowData.name,
          "onUpdate:modelValue": (val) => {
            rowData.name = val;
          },
          onInput: (val) => {
            console.log(val);
          },
        },
        {}
      ),
    width: 150,
    align: "center",
  },
];

const data = ref<tableData[]>([]);
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

<template>
  <el-table-v2
    :columns="columns"
    :data="data"
    :width="700"
    :height="400"
    fixed
  />
</template>
