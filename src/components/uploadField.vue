<template>
  <div class="inputs-wrapper">
    <input type="file" disabled hidden />
    <input type="text" class="input-text" />
    <button type="submit" class="insert-button">Insert</button>
  </div>
</template>

<style scoped>
.inputs-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}
.input-text {
  min-width: 20rem;
  height: 3.2rem;
  border-radius: 5px 0px 0px 5px;
  background: rgba(0, 255, 170, 0.075);
  border-style: solid;
  border-width: 3px;
  border-color: hsla(160, 100%, 37%, 1);
  outline: none;
  transition-duration: 200ms;
  color: white;
  text-overflow: ellipsis;
}
.input-text:hover {
  background: rgba(0, 255, 170, 0.274);
}
.insert-button {
  cursor: pointer;
  font-size: 1rem;
  height: 3.2rem;
  background-color: hsla(160, 100%, 37%, 1);
  border: none;
  color: white;
  border-radius: 0px 4px 4px 0px;
  padding: 0 2rem 0 2rem;
  font-weight: bold;
  transition-duration: 100ms;
}
.insert-button:hover {
  background-color: rgb(34, 212, 153);
}
</style>
<script setup lang="ts"></script>
