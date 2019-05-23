<!-- 
 Original source: https://alligator.io/vuejs/file-reader-component/
 Original author: Alex Jover Morales (https://alligator.io/author/alex-jover-morales)
 Modified by jamcha (https://github.com/jamcha-aa)
 (c) 2018 Alex Jover Morales, (c) 2019 Alligator.io., (c) 2019 jamcha.
 License: MIT License
-->

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
  top: 0;
  right: 0;
  z-index: -1;
  opacity: 0;
}
</style>
