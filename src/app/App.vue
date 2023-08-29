<script setup>
import { ref } from 'vue';
import PostForm from './user/PostForm.vue';
import PostList from './user/PostList.vue';
import MyInput from './user/UI/MyInput.vue';

const pgpSize = 3335 // см^2
const pgpWeight = 36 // кг
let gapSize = ref([
    { id: 1, width: 90, height: 205 },
])

let wallWidth = ref('')
let wallHeight = ref('')


function removePost(gap){
    gapSize.value = gapSize.value.filter(p => p.id !== gap.id)
}

function createPost(gap){
    gapSize.value.push(gap)
}

function getSquare(){
    wallHeight.value * wallWidth.value * 10000
}

</script>

<template>
  <div class="app">
    <div class="container">
    <h1 class="app__title">Введите высоту и ширину стены</h1>
    <label class="app__label" for="height">Высота стены:</label>
        <MyInput 
        id="height"
        v-model:value="wallHeight" 
        type="number" 
        placeholder="Высота"
        />
        <label class="app__label" for="width">Ширина стены:</label>
        <MyInput
        id="width"
        v-model:value="wallWidth" 
        type="number" 
        placeholder="Ширина"
        />
        <h2 class="app__title">Введите ширину и высоту проёма</h2>
     <PostForm 
      @create="createPost"
      />
      <PostList 
      :gapSize="gapSize"
      @remove="removePost"
      />
      <h2 class="app__title">Общие параметры</h2>
      <section class="app__container">
          <p><b>Это количество плит:</b> {{ Math.ceil((wallHeight * wallWidth * 10000 - gapSize.reduce((accum,item) => accum + item.width * item.height, 0)) / pgpSize) }} шт</p>
          <p><b>Это масса стены:</b> {{ pgpWeight * Math.ceil((wallHeight * wallWidth * 10000 - gapSize.reduce((accum,item) => accum + item.width * item.height, 0)) / pgpSize) }} кг</p>
        </section>
  </div>
</div>
</template>

<style>
@import "./index.scss";

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  .app {
    background-color: #1c1e21;
    color: rgba(255, 255, 255, .87)
  }

  .app__container {
    border: 1px solid #fff;
    border-radius: 5px;
    padding: 25px;
    padding-left: 15px;
  }

  .app__label{
    font-size: 18px;
  }

  .app__title {
    margin-top: 15px;
    margin-bottom: 15px;
    text-align: center;
  }

  .container {
    margin: 0 auto;
    width: 770px;
    background-color: #242424;
    padding: 10px 30px;
  }

</style>