<template>
  <div class="wrapper">
    <div
      class="backdrop"
      @click="onClose"
    ></div>
    <div class="container">
      <button
        class="close-button"
        @click="onClose"
      >
        <svg viewBox="0 0 24 24">
          <path
            d="M19,6.41L17.59,5L12,10.59L6.41,5L5,6.41L10.59,12L5,17.59L6.41,19L12,13.41L17.59,19L19,17.59L13.41,12L19,6.41Z"
          />
        </svg>
      </button>
      <h1>{{ itemData.attributes.canonicalTitle }}</h1>
      <div class="image-sinopsis-container">
        <img :src="itemData.attributes.posterImage.original" />
        <h4>{{ itemData.attributes.synopsis }}</h4>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'InfoModal',
  methods: {
    onClose() {
      this.$emit('onClose');
    },
  },
  props: { itemData: Object },
};
</script>

<style scoped>
.wrapper {
  position: fixed;
  height: 100vh;
  width: 100vw;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10000;
}
.backdrop {
  height: 100vh;
  width: 100vw;
  background-color: rgba(0, 0, 0, 0.7);
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
}

.container {
  max-width: 784px;
  width: calc(100% - 16px);
  background-color: white;
  height: calc(100% - 64px);
  z-index: 1;
  border-radius: 16px;
  position: relative;
  padding: 16px;
  box-sizing: border-box;
}
h1 {
  text-align: left;
}

img {
  width: 200px;
  object-fit: contain;
}

.image-sinopsis-container {
  display: flex;
  justify-content: center;
}
.close-button {
  position: absolute;
  top: 16px;
  right: 16px;
  background: none;
  border: none;
}

.close-button > svg {
  height: 32px;
  width: 32px;
}
</style>
