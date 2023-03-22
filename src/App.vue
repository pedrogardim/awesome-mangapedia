<template>
  <SearchBar @onSearch="onSearch" />
  <LoadingSpinner v-if="isLoading" />
  <MangaList
    v-if="mangaData.length > 0 && !isLoading"
    :mangaData="mangaData"
    @onItemClick="openManga"
  />
  <InfoModal
    v-if="openedItem"
    :itemData="openedItem"
    @onClose="onMangaClose"
  />
</template>

<script>
import axios from 'axios';
import { debounce } from 'debounce';
import SearchBar from './components/SearchBar.vue';
import MangaList from './components/MangaList.vue';
import InfoModal from './components/InfoModal.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

export default {
  name: 'App',
  data() {
    return { mangaData: [], isLoading: false, openedItem: null };
  },
  methods: {
    async onSearch(text) {
      this.isLoading = true;
      debounce(async () => {
        console.log('query');
        const result = await axios.get(
          `https://kitsu.io/api/edge/manga?filter[text]=${text}&sort=popularityRank,-userCount`
        );

        this.mangaData = result.data.data;
        this.isLoading = false;
      }, 500)();
    },
    openManga(item) {
      this.openedItem = item;
    },
    onMangaClose() {
      this.openedItem = null;
    },
  },
  watch: {
    openedItem(newItem) {
      console.log(newItem);
    },
  },
  components: {
    SearchBar,
    MangaList,
    InfoModal,
    LoadingSpinner,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
