<template>
  <div class="box">
    <div>
      <p>
        {{ gunluk.diary }}
      </p>
      <small class="date"> {{ gunluk.date }} </small>
    </div>
    <div>
      <i
        class="material-symbols-outlined"
        :class="{ active: gunluk.isFav }"
        @click="diaryStore.toggleFav(gunluk.id)"
      >
        star
      </i>
      <i
        class="material-symbols-outlined"
        @click="diaryStore.deleteDiary(gunluk.id)"
      >
        delete
      </i>
    </div>
  </div>
</template>

<script>
import { useDiaryStore } from "../stores/DiaryStore";

export default {
  props: ["gunluk"],
  setup() {
    const diaryStore = useDiaryStore();
    return { diaryStore };
  },
};
</script>
