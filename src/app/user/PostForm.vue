<template>
      <form class="app__form" @submit.prevent>
        <label class="app__label" for="height">Ширина проёма:</label>
        <MyInput 
        id="height"
        v-model:value="gap.width" 
        type="number" 
        placeholder="Высота"
        />
        <label class="app__label" for="width">Высота проёма:</label>
        <MyInput
        id="width"
        v-model:value="gap.height" 
        type="number" 
        placeholder="Ширина"
        />
        <MyButton
        class="app__button"
        @click="createPost"
        >
        Создать
        </MyButton>
      </form>
  </template>

<script>
import MyInput from './UI/MyInput.vue';
import MyButton from './UI/MyButton.vue';

export default {
    data() {
        return {
            gap: {
                width: '',
                height: ''
            }
        };
    },
    methods: {
        createPost() {
            this.gap.id = Date.now();
            this.$emit('create', this.gap);
            this.gap = {
                width: '',
                height: ''
            };
        },
    },
    components: { MyInput, MyButton }
}

</script>
  
  <style scoped>
  .app__form {
    margin-top: 20px;
    display: grid;
    grid-template-columns: 200px 1fr;
    row-gap: 10px;
  }
  .app__label {
    display: block;
    background-color: #fff;
    color: #000;
    font-weight: 700;
    padding: 10px;
    border-radius: 5px 0 0 5px;
  }
  .app__button {
    align-self: center;
    margin-top: 15px;
  }
  </style>