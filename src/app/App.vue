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
  if(gap.width > 0 && gap.height > 0){
    gapSize.value.push(gap)
  }
}

function getSquare(){
    return wallHeight.value * wallWidth.value ===0
}

function getAmountOfPgp(){
  return Math.ceil((wallHeight.value * wallWidth.value * 10000 - gapSize.value.reduce((accum,item) => accum + item.width * item.height, 0)) / pgpSize)
}

function getCheckWallSize(){
  return wallHeight.value > 0 && wallWidth.value > 0
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
        placeholder="Высота, [м]"
        />
        <label class="app__label" for="width">Ширина стены:</label>
        <MyInput
        id="width"
        v-model:value="wallWidth" 
        type="number" 
        placeholder="Ширина, [м]"
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
      <section class="app__container" v-if="getAmountOfPgp() > 0 && getCheckWallSize()">
          <p><b>Это количество плит:</b> {{ getAmountOfPgp() }} шт</p>
          <p><b>Это масса стены:</b> {{ pgpWeight * getAmountOfPgp() }} кг</p>
      </section>
      <h3 v-else-if="getSquare()" class="not-size">Введите размеры стены</h3>
      <h3 v-else class="error">У вас слишком много проёмов или неккоректно введены данные!</h3>
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
  .error {
    border: 1px solid red;
    color: red;
    padding: 25px 15px;
  }
  .not-size {
    border: 1px solid rgb(178, 2, 134);
    color: rgb(178, 2, 134);
    padding: 25px 15px;
  }
</style>