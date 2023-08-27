<template>
    <div class="post">
        <div>
            <div class="post__item"><strong>Ширина проёма:</strong><span>{{ gap.width }} см</span></div>
            <div class="post__item"><strong>Высота проёма:</strong><span>{{ gap.height }} см</span></div>
        </div>
        <div class="post__btns">
            <MyButton
            @click="$emit('remove', gap)"
            >Удалить</MyButton>
        </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';
import MyButton from './UI/MyButton.vue';
defineProps({
    gap: {
        type: Object,
        required: true
    }
})
</script>
    
<style scoped>
.post {
    padding: 15px;
    border: 1px solid #fff;
    margin-top: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.post__item {
    width: 300px;
    display: flex;
    justify-content: space-between;
}
.post__btns {
    margin-top: 0;
}
</style>