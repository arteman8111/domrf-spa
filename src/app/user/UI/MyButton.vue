<template>
    <button class="btn">
        <slot></slot>
    </button>
</template>

<script setup>

</script>

<style lang="scss" scoped>
.btn {
  padding: 10px 15px;
  background: none;
  color: #fff;
  border: 1px solid #fff;
  font-size: 18px;
  font-weight: 700;
  transition: all ease 0.3s;

  &:hover {
    background-color: #fff;
    color: #1c1e21;
  }
}

</style>