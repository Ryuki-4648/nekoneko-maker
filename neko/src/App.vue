<script setup>
import PageTitle from './components/PageTitle.vue'
import { ref } from 'vue';
import CatImageSVGComponent from './components/CatImage.vue'

const name = ref('');
// const rotate = ref(0);
const catBodyColor = ref('#fafafa');
const backgroundColor = ref('#fee1e1');
const showFood01 = ref(false);
const showFood02 = ref(false);
const showFood03 = ref(false);
const resetButton = () => {
  name.value = '';
  catBodyColor.value = '#fafafa';
  backgroundColor.value = '#fee1e1';
  showFood01.value = false;
  showFood02.value = false;
  showFood03.value = false;
}
</script>
<!-- script setup コンポーネントのロジックを設定 -->

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="80" height="80" />
  </header>

  <main>
    <PageTitle msg="ねこねこメーカー" />

    <div class="content">
      <section>
        <div class="area-cat" v-bind:style="{backgroundColor: backgroundColor}">
          <CatImageSVGComponent class="image-cat" v-bind:style="{fill: catBodyColor, stroke: '#000'}" />
          <img v-if="showFood01" class="food01" src="./assets/img/image-food01.svg" alt="" />
          <img v-if="showFood02" class="food02" src="./assets/img/image-food02.svg" alt="" />
          <img v-if="showFood03" class="food03" src="./assets/img/image-food03.svg" alt="" />
          <p class="text01"><span v-if="name">{{ name }} です！</span><span v-else></span></p>
        </div>
      </section>

      <section>
        <p v-bind:style="{ display: 'inline-block', catBodyColor: catBodyColor }"></p>
        <p class="text01"><span v-if="name"></span><span v-else>なまえを入力する</span></p>
        <p><input type="text" v-model="name" class="input-name"></p>
        
        <!-- <div class="area-turn">
          <p>回してみる</p>
          <input type="range" name="range" v-model="rotate" min="0" step="0.01" max="1">
          <p>{{ rotate }} turn</p>
        </div> -->

        <div class="area-color">
          <p class="text-picker">カラーピッカーで毛色を選択する</p>
          <input type="color" name="color" v-model="catBodyColor">
          <p class="color-code">カラーコード: {{ catBodyColor }}</p>
        </div>

        <div class="area-food">
          <p>好きなエサを置いてください</p>
          <ul class="list-foods">
            <li>
              <input type="checkbox" id="food01" name="scales" checked v-model="showFood01" />
              <label for="food01">ネコプチ | おいしい煮干しセット</label>
            </li>
            <li>
              <input type="checkbox" id="food02" name="scales" checked v-model="showFood02" />
              <label for="food02">金のスプーン | ささみたっぷり味わいブレンド</label>
            </li>
            <li>
              <input type="checkbox" id="food03" name="scales" checked v-model="showFood03" />
              <label for="food03">ネコチャーム | にゃんともおいしいかつお入りフード</label>
            </li>
          </ul>
        </div>

        <div class="area-color">
          <p class="text-picker">壁紙を変える</p>
          <input type="color" name="color" v-model="backgroundColor">
          <p class="color-code">カラーコード: {{ backgroundColor }}</p>
        </div>

        <button @click="resetButton">リセットする</button>
      </section>
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
  max-width: 800px;
  padding: 0 20px;
  margin: 0 auto;
}
header {
  position: absolute;
  top: 12px;
  left: 12px;
}
.content {
  display: flex;
  justify-content: space-between;
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
  position: absolute;
  width: 280px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.text01 {
  margin: 0 auto 10px;
  height: 22px;
}
.text-picker {
  margin: 0 auto 10px;
}
.color-code {
  font-size: 13px;
}
.food01, .food02, .food03 {
  position: absolute;
}
.food01 {
  bottom: 20px;
  right: 10px;
  width: 70px;
}
.food02 {
  bottom: 25px;
  left: 140px;
  width: 60px;
}
.food03 {
  bottom: 8px;
  left: 10px;
  width: 70px;
}
.area-cat {
  width: 320px;
  height: 320px;
  margin: 0 auto;
  padding: 10px;
  position: relative;
}
.area-turn, .area-food {
  margin: 0 auto 40px;
}
.list-foods input, .list-foods label {
  cursor: pointer;
}
input[type="color"] {
  border: none;
  outline: none;
  width: 180px;
  height: 40px;
  cursor: pointer;
}
.image-cat path {
  fill:#fafafa;
  stroke:#000;
  stroke-linecap:round;
  stroke-linejoin:round;
  stroke-width:6px;
}
</style>
