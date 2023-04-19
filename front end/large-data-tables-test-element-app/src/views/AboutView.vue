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
  <el-table :data="data" style="width: 100%" :max-height="500">
    <el-table-column prop="id" label="id" width="180" />
    <el-table-column prop="name" label="Name" width="180" />
    <el-table-column prop="index" label="index" width="180" />
    <el-table-column label="Operations">
      <template #default="scope">
        <el-button size="small" @click="scope.row.index++"> Edit </el-button>
      </template>
    </el-table-column>
    <el-table-column prop="index" label="operations" width="180">
      <el-input />
    </el-table-column>
  </el-table>
</template>
