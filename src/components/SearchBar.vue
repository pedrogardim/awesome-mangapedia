<template>
  <div class="container">
    <input
      type="text"
      @input="onInput"
    />
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  methods: {
    onInput(event) {
      this.$emit('onSearch', event.target.value);
    },
  },
};
</script>

<style scoped>
div {
  margin: 32px;
}
input {
  font-size: 40px;
  border-radius: 0;
  border: 1px solid rgba(0, 0, 0, 0.3);
}

input:focus {
  outline: none;
}
</style>
