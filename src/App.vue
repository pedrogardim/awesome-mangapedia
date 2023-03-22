<template>
  <SearchBar @onSearch="onSearch" />
  <MangaList
    :mangaData="mangaData"
    @onItemClick="openManga"
  />
</template>

<script>
import axios from 'axios';
import { debounce } from 'debounce';
import SearchBar from './components/SearchBar.vue';
import MangaList from './components/MangaList.vue';

export default {
  name: 'App',
  data() {
    return { mangaData: [], isLoading: false };
  },
  methods: {
    async onSearch(text) {
      this.isLoading = true;
      debounce(async () => {
        const result = await axios.get(
          `https://kitsu.io/api/edge/manga?filter[text]=${text}&sort=popularityRank,-userCount`
        );

        this.mangaData = result.data.data;
        this.isLoading = false;
      }, 500)();
    },
    openManga(item) {
      this.openedItem = item;
      console.log(item);
    },
  },
  components: {
    SearchBar,
    MangaList,
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
