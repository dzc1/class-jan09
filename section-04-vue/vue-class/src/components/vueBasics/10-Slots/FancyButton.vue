<template>
  <button class="fancy-btn">
    <slot />
  </button>
</template>

<style>
.fancy-btn {
  color: #fff;
  background: black;
  border: none;
  padding: 5px 10px;
  margin: 5px;
  border-radius: 8px;
  cursor: pointer;
}

.black {
  background: green;
  color: black;
}
</style>

<script setup></script>
