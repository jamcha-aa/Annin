<template>
  <label class="text-reader">
    🗁
    <input type="file" @change="loadTextFromFile">
  </label>
</template>

<script>
export default {
  methods: {
    loadTextFromFile(ev) {
      const file = ev.target.files[0];
      const reader = new FileReader();

      reader.onload = e => this.$emit("load", e.target.result);
      reader.readAsText(file);
    }
  }
};
</script>

<style>
.text-reader input {
  position: absolute;
  z-index: -1;
  opacity: 0;
}
</style>
