<template>
  <div>
    <h2 class="title">Количество проёмов</h2>
    <PostItem
    v-for="gap in gapSize"
    :gap="gap"
    :key="gap.id"
    @remove="$emit('remove', gap)"
    />
  </div>
</template>
  
<script setup>
import PostItem from './PostItem.vue';


defineProps({
  gapSize: {
    type: Array,
    required: true
  }
})

</script>
  
<style scoped>
  .title {
    text-align: center;
    margin-top: 15px;
  }
</style>