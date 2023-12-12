<template>
  <MyForm :addrow="addRow" />
  <MyTable :tabledata="tableData" />
</template>

<script setup lang="ts">
import { ref } from "vue";
import MyForm from "@/components/MyForm.vue";
import MyTable from "@/components/MyTable.vue";
import { TableData } from "@/components/MyTable.vue";

const tableData = ref<TableData[]>([]);

const addRow = (newRow: TableData) => {
  tableData.value.push(newRow);
};
</script>
