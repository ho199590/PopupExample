<template>
  <button @click="toggle">글 작성하기</button>
  <Transition name="modal">
    <div v-if="show" class="modal-mask">
      <div class="modal-container">
        <div class="modal-header">게시글 내용 입력</div>
        <hr />
        <div class="modal-body">
          <div>제목: <input v-model.trim="newRow.title" maxlength="20" /></div>
          <hr />
          <div>내용: <textarea v-model="newRow.content" /></div>
          <hr />
          <div>
            작성자:
            <select v-model="newRow.writer">
              <option disabled value="">사용자 설정</option>
              <option>noh</option>
              <option>jin</option>
              <option>ho</option>
            </select>
          </div>
          <hr />
        </div>
        <div class="modal-footer">
          <button @click="submitRow">작성</button>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script setup lang="ts">
import { defineProps, ref } from "vue";
import { TableData } from "@/components/MyTable.vue";

const props = defineProps<{ addrow: (newRow: TableData) => void }>();
const show = ref(false);

function toggle() {
  show.value = !show.value;
}

const newRow = ref<TableData>({
  title: "",
  content: "",
  writer: "",
  wdate: new Date(),
});

const submitRow = () => {
  props.addrow({ ...newRow.value });
  show.value = !show.value;
  // 모달을 닫고 입력 내용 초기화
  newRow.value = {
    title: "",
    content: "",
    writer: "",
    wdate: new Date(),
  };
};
</script>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  transition: opacity 0.3s ease;
}

.modal-container {
  width: 300px;
  margin: auto;
  padding: 20px 30px;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
}

.modal-body {
  margin: 20px 0;
}
</style>
