<template>
  <div class="container">
    <MangaListItem
      v-for="manga in mangaData"
      :manga="manga"
      :key="manga.id"
      @onClick="onItemClick"
    />
  </div>
</template>

<script>
import MangaListItem from './MangaListItem.vue';

export default {
  name: 'MangaList',
  methods: {
    onInput(event) {
      this.$emit('onSearch', event.target.value);
    },
    onItemClick(manga) {
      this.$emit('onItemClick', manga);
    },
  },
  components: { MangaListItem },
  props: { mangaData: Array },
};
</script>

<style scoped>
.container {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-items: center;
  max-width: 784px;
}
</style>
