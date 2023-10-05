<script setup>
import PageTitle from './components/PageTitle.vue'
import { ref } from 'vue';
import CatImageSVGComponent from './components/CatImage.vue'

const name = ref('');
const rotate = ref(0);
const catBodyColor = ref('#fafafa');
const backgroundColor = ref('#fafafa');
</script>
<!-- script setup コンポーネントのロジックを設定 -->

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="80" height="80" />
  </header>

  <main>
    <div>
      <PageTitle msg="ねこねこメーカー" />
      <CatImageSVGComponent class="image-cat" />
      <p v-bind:style="{ display: 'inline-block', catBodyColor: catBodyColor }"></p>
      <p class="text01"><span v-if="name">{{ name }} です！</span><span v-else>おなまえを入力してください。</span></p>
      <p><input type="text" v-model="name" class="input-name"></p>
      
      <div class="area-turn">
        <p>回してみる</p>
        <input type="range" name="range" v-model="rotate" min="0" step="0.01" max="1">
        <p>{{ rotate }} turn</p>
      </div>

      <div class="area-color">
        <p class="text-picker">カラーピッカーで毛色を選択する</p>
        <input type="color" name="color" v-model="catBodyColor">
        <p class="color-code">カラーコード: {{ catBodyColor }}</p>
      </div>

      <div class="area-food">
        <p>エサを置く</p>
        <ul>
          <li>
            <input type="checkbox" id="food01" name="scales" checked />
            <label for="food01">えさ1</label>
          </li>
          <li>
            <input type="checkbox" id="food02" name="scales" checked />
            <label for="food02">えさ2</label>
          </li>
          <li>
            <input type="checkbox" id="food03" name="scales" checked />
            <label for="food03">えさ3</label>
          </li>
        </ul>
      </div>

      <div class="area-color">
        <p class="text-picker">壁紙を変える</p>
        <input type="color" name="color" v-model="backgroundColor">
        <p class="color-code">カラーコード: {{ backgroundColor }}</p>
      </div>

    </div>
  </main>
</template>
<!-- v-model を使用してデータバインディングを行う。 -->

<style scoped>
h1 {
  font-size: 24px;
}
h2 {
  font-size: 18px;
  margin: 0 auto 40px;
}
main {
  max-width: 600px;
  padding: 0 20px;
  margin: 0 auto;
}
header {
  position: absolute;
  top: 12px;
  left: 12px;
}
.input-name {
  border: 2px solid #dadada;
  height: 56px;
  width: 400px;
  border-radius: 30px;
  padding: 2px 2px 2px 12px;
  font-size: 14px;
  margin: 0 auto 60px;
}
.image-cat {
  margin: 0 auto 40px;
  width: 200px;
  height: 200px;
}
.text01 {
  margin: 0 auto 14px;
}
.text-picker {
  margin: 0 auto 14px;
}
.color-code {
  font-size: 13px;
}
.area-turn, .area-food {
  margin: 0 auto 40px;
}
input[type="color"] {
  border: none;
  outline: none;
  width: 180px;
  height: 40px;
  cursor: pointer;
}
.cls-1{fill:none;stroke:#000;stroke-linecap:round;stroke-linejoin:round;stroke-width:6px;}
</style>
