<template>
  <form @submit.prevent="sendForm">
    <div class="box">
      <div class="form-group">
        <textarea v-model="newDiary" placeholder="bugün neler oldu?"></textarea>
        <button>günlüğü kaydet</button>
      </div>
    </div>
  </form>
</template>

<script>
import { ref } from "vue";
import { useDiaryStore } from "../stores/DiaryStore";

export default {
  setup() {
    const diaryStore = useDiaryStore();
    const newDiary = ref("");
    const currentDate = () => {
      const current = new Date();
      const date =
        current.getDate() +
        "." +
        (current.getMonth() + 1) +
        "." +
        current.getFullYear();
      return date;
    };
    const sendForm = () => {
      if (newDiary.value.length > 0) {
        diaryStore.newDiary({
          id: diaryStore.diary.length + 1,
          diary: newDiary.value,
          date: currentDate(),
          isFav: false,
        });
        newDiary.value = "";
      }
    };
    return { sendForm, newDiary };
  },
};
</script>
