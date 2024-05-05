<template>
  <header>
    <div class="container">
      <img src="./assets/pinia-logo.svg" alt="Pinia" title="Pinia" />
      <h1>Kişisel Günlüğüm</h1>
    </div>
  </header>
  <main>
    <div class="container">
      <NewDiary></NewDiary>

      <div class="data-area">
        <p v-if="filter === 'favs'">toplam {{ favCount }} kayıt var</p>
        <p v-if="filter === 'all'">toplam {{ totalCount }} kayıt var</p>

        <div>
          <button style="cursor: pointer" @click="filter = 'all'">
            Tüm günlüklerim
          </button>
          <button style="cursor: pointer" @click="filter = 'favs'">
            Sadece beğendiklerim
          </button>
          <button
            style="cursor: pointer; background-color: red; color: white"
            @click="gunlukStore.$reset"
          >
            Tüm Günlükleri Sil
          </button>
        </div>
      </div>
      <div
        class="gunluk-listesi"
        v-for="gunluk in diary"
        v-if="filter === 'all'"
      >
        <GunlukDetail :gunluk="gunluk"></GunlukDetail>
      </div>
      <div
        class="gunluk-listesi"
        v-for="gunluk in favs"
        v-if="filter === 'favs'"
      >
        <GunlukDetail :gunluk="gunluk"></GunlukDetail>
      </div>
    </div>
  </main>
</template>

<script>
import { ref } from "vue";
import GunlukDetail from "./components/gunluk-detail.vue";
import { useDiaryStore } from "./stores/DiaryStore";
import NewDiary from "./components/yeni-gunluk.vue";
import { storeToRefs } from "pinia";
export default {
  components: {
    GunlukDetail,
    NewDiary,
  },
  setup() {
    const gunlukStore = useDiaryStore();
    const filter = ref("all");
    const { diary, loading, favs, totalCount, favCount } =
      storeToRefs(gunlukStore);
    gunlukStore.getDiary();
    return { gunlukStore, filter, diary, loading, favs, totalCount, favCount };
  },
};
</script>
