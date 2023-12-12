<template>
  <table>
    <thead>
      <tr>
        <th>제목</th>
        <th>내용</th>
        <th>작성자</th>
        <th>작성일</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="row in tabledata" :key="row.title">
        <td>{{ row.title }}</td>
        <td>{{ row.content }}</td>
        <td>{{ row.writer }}</td>
        <td>{{ formatDate(row.wdate) }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script setup lang="ts">
import { defineProps, onMounted, onUpdated } from "vue";

export interface TableData {
  title: string;
  content: string;
  writer: string;
  wdate: Date;
}

const props = defineProps<{ tabledata: TableData[] }>();
onMounted(() => {
  console.log("tableData onMounted : ", props.tabledata.values);
});
onUpdated(() => {
  console.log("tableData onUpdated : ", props.tabledata.values);
});

const formatDate = (dateString: string | number | Date) => {
  const date = new Date(dateString);
  return (
    date
      .toLocaleString("ko-KR", {
        year: "numeric",
        month: "2-digit",
        day: "2-digit",
        hour: "2-digit",
        minute: "2-digit",
      })
      .replace("년 ", "년")
      .replace("일 ", "일")
      .replace(":", "시 ") + "분"
  );
};
</script>

<style scoped>
table th,
table td {
  border: solid black 1px;
}
</style>
