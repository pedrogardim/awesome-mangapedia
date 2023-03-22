<template>
  <div
    class="manga-item"
    @click="onClick"
  >
    <img :src="getPoster" />
  </div>
</template>

<script>
export default {
  name: 'MangaListItem',
  computed: {
    getPoster() {
      return this.manga.attributes.posterImage.original;
    },
  },
  methods: {
    onClick() {
      this.$emit('onClick', this.manga);
    },
  },
  props: { manga: Object },
};
</script>

<style scoped>
.manga-item {
  margin: 8px;
  box-shadow: 0px 0px 8px 2px rgba(0, 0, 0, 0.312);
  flex: 1 1 30%;
  max-width: 33%;
  aspect-ratio: 1 / 1.5;
  position: relative;
  overflow: hidden;
}

.manga-item:hover > img {
  filter: brightness(0.4);
  transform: scale(1.1);
}

.manga-item > img {
  width: 100%;
  height: 100%;
  position: absolute;
  overflow: hidden;
  top: 0;
  left: 0;
  z-index: -1;
  transition: all 0.3s;
}
</style>
