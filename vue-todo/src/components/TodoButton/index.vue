<script setup></script>

<template>
  <button>
    <slot> Create </slot>
  </button>
</template>

<style lang="scss" scoped>
button {
  color: #fff;
  background-color: #2b8b61;
  outline: none;
  border: none;
  padding: 0.3rem 1rem;
  cursor: pointer;
  transition: 100ms;

  &:hover {
    background-color: #165f3f;
  }
}
</style>
