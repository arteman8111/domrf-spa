<template>
    <input :value="value" @input="$emit('update:value', $event.target.value)" class="input" type="text" min="0">
</template>

<script setup>
defineProps({
    value: [String, Number]
})

</script>

<style lang="scss" scoped>
.input {
    width: 100%;
    padding: 10px 15px;
    background-color: #1c1e21;
    border: 1px solid #fff;
    color:#fff;
    font-size: 18px;
    text-align: center;
}

.input::placeholder {
    color:rgba($color: #fff, $alpha: 0.3);
}
</style>