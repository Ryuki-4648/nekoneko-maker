<script setup>
import PageTitle from './components/PageTitle.vue'
import { ref } from 'vue';
import CatImageSVGComponent from './components/CatImage.vue'

const name = ref('');
const isCatNameTooLong = ref(false);

const checkCatNameLength = () => {
  name.value = name.value.slice(0, 13); // 13文字を超える部分を削除
  if (name.value.length > 13) {
    isCatNameTooLong.value = true;
  } else {
    isCatNameTooLong.value = false;
  }
};

// カラー
const catBodyColor = ref('#fafafa');
const backgroundColor = ref('#fee1e1');

// エサを置く
const showFood01 = ref(false);
const showFood02 = ref(false);
const showFood03 = ref(false);

// ねこの顔
const openEyes = ref(true);
const closeEyes = ref(false);
const eyeState = ref('openEyes');

const resetButton = () => {
  name.value = '';
  catBodyColor.value = '#fafafa';
  backgroundColor.value = '#fee1e1';
  showFood01.value = false;
  showFood02.value = false;
  showFood03.value = false;
  openEyes.value = true;
  closeEyes.value = false;
  showToy01.value = false;
}

// ご機嫌モード（ねこ3回クリックで音符が出る）
const imageCatClickCount = ref(0);
const icon01 = ref(false);
const handleImageCatClick = () => {
  imageCatClickCount.value++;
  if (imageCatClickCount.value >= 3) {
    icon01.value = true;
  }
};

// おもちゃのボタン
const showToy01 = ref(false);
const handleToyButton01 = () => {
  showToy01.value = true;
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
      <section class="drawing">
        <div class="area-cat" v-bind:style="{backgroundColor: backgroundColor}">
          <CatImageSVGComponent
            class="image-cat"
            v-bind:style="{fill: catBodyColor, stroke: '#000'}"
            @click="handleImageCatClick"
          />
          <img v-if="showFood01" class="food01" src="./assets/img/image-food01.svg" alt="" />
          <img v-if="showFood02" class="food02" src="./assets/img/image-food02.svg" alt="" />
          <img v-if="showFood03" class="food03" src="./assets/img/image-food03.svg" alt="" />
          <img class="cat-parts01" src="./assets/img/image-cat01.svg" alt="" />
          <img v-if="eyeState === 'openEyes'" class="cat-parts02" src="./assets/img/image-cat02.svg" alt="" />
          <img v-if="eyeState === 'closeEyes'" class="cat-parts03" src="./assets/img/image-cat03.svg" alt="" />
          <img v-if="icon01" class="icon01" src="./assets/img/icon01.svg" />
          <img v-if="showToy01" src="./assets/img/toy01.png" class="image-toy01" />
        </div>
        <ul class="list-toys">
          <li class="item-toys01" @click="handleToyButton01"><img src="./assets/img/toy01.png" /></li>
          <li class="item-toys02"><img src="./assets/img/toy02.png" /></li>
          <li class="item-toys03"><img src="./assets/img/toy03.png" /></li>
        </ul>
        <div class="area-text-name">
          <p v-if="name" class="text-name">{{ name }}</p><p v-else></p>
        </div>
      </section>

      <section class="detail">
        <div class="detail-scroll">
          <div class="detail-box">
            <p v-bind:style="{ display: 'inline-block', catBodyColor: catBodyColor }"></p>
            <p class="text01">なまえを入力する（13文字以内）</p>
            <p><input type="text" v-model="name" class="input-name" @input="checkCatNameLength"></p>
            <p class="text-alert" v-if="isCatNameTooLong">13文字以内で入力してください。</p>
            
            <!-- <div class="area-turn">
              <p>回してみる</p>
              <input type="range" name="range" v-model="rotate" min="0" step="0.01" max="1">
              <p>{{ rotate }} turn</p>
            </div> -->

            <div class="area-color">
              <p class="text-picker text01">カラーピッカーで毛色を選択する</p>
              <input type="color" name="color" v-model="catBodyColor">
              <p class="color-code">カラーコード: {{ catBodyColor }}</p>
            </div>

            <div class="area-food">
              <p class="text01">好きなエサを置く</p>
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

            <div>
              <p class="text01">眠気具合を選ぶ</p>
              <ul class="list-face">
                <li>
                  <input type="radio" id="openEyes" name="eyeState" value="openEyes" checked v-model="eyeState" />
                  <label for="openEyes">ねむくない</label>
                </li>
                <li>
                  <input type="radio" id="closeEyes" name="eyeState" value="closeEyes" v-model="eyeState" />
                  <label for="closeEyes">ねむい</label>
                </li>
              </ul>
            </div>

            <div class="area-color">
              <p class="text-picker">壁紙を変える</p>
              <input type="color" name="color" v-model="backgroundColor">
              <p class="color-code">カラーコード: {{ backgroundColor }}</p>
            </div>

            <button @click="resetButton" class="button-reset">リセットする</button>
          </div>
        </div>
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
  max-width: 850px;
  padding: 0 20px;
  margin: 0 auto;
}
header {
  position: absolute;
  top: 12px;
  left: 12px;
}
.logo {
  position: fixed;
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
  cursor: pointer;
}
.text01 {
  margin: 0 auto 8px;
  font-size: .95rem;
  font-weight: bold;
  letter-spacing: .03em;
}
.area-text-name {
  margin: 20px auto 0;
  border: 3px solid #161616;
  border-radius: 30px;
  height: 48px;
  width: 320px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2px 4px;
}
.text-name {
  font-size: 1.3rem;
  font-weight: bold;
  text-align: center;

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
.cat-parts01, .cat-parts02, .cat-parts03 {
  position: absolute;
  z-index: 10;
}
.cat-parts01 {
  width: 18px;
  left: 92px;
  top: 134px;
}
.cat-parts02 {
  width: 34px;
  left: 85px;
  top: 124px;
}
.cat-parts03 {
  width: 34px;
  left: 85px;
  top: 126px;
}
.area-cat {
  width: 320px;
  height: 320px;
  padding: 10px;
  position: relative;
  border: 3px solid #161616;
  border-radius: 20px;
}
.area-cat {
  margin: 0 auto 20px;
}
.area-turn, .area-food, .area-color {
  margin: 0 auto 40px;
}
.list-foods input, .list-foods label, .list-face label {
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
.detail {
  border: 3px solid #161616;
  border-radius: 20px;
  padding: 16px 16px 16px 0;
}
.detail-scroll {
  overflow-y: scroll;
}
.detail-box {
  height: 400px;
  padding: 0 20px;
}
.button-reset {
  width: 160px;
  height: 36px;
  border: none;
  background-color: #eaeaea;
  margin-bottom: 40px;
  cursor: pointer;
  transition: all .3s;
}
.button-reset:hover {
  background-color: #dadada;
}
.detail-scroll::-webkit-scrollbar {
  width: 14px;
  border-radius: 10px;
}
.detail-scroll::-webkit-scrollbar-track {
  background-color: #eaeaea;
}
.detail-scroll::-webkit-scrollbar-thumb {
  background-color: #fee1e1;
}
.icon01 {
  width: 20px;
  position: absolute;
  left: 24px;
  top: 86px;
}
.list-toys {
  display: flex;
  justify-content: space-between;
}
.list-toys li {
  border-radius: 50%;
  border: 3px solid #161616;
  width: 70px;
  height: 70px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #fee1e1;
  cursor: pointer;
  transition: all .3s;
}
.list-toys li:hover {
  background-color: #f5c2c2;
}
.item-toys01 img {
  width: 20px;
}
.item-toys02 img {
  width: 50px;
}
.item-toys03 img {
  width: 50px;
}
.image-toy01 {
  position: absolute;
  left: 40px;
  top: 130px;
  width: 30px;
  animation: toy01animation 2s linear infinite;
}
@keyframes toy01animation {
  0% , 100%{
    transform: rotate(10deg);
  }
  50%{
    transform: rotate(-10deg);
  }
}
@media screen and (max-width: 900px) {
  .drawing {
    width: 320px;
    margin: 0 auto 30px;
  }
  .content {
    flex-wrap: wrap;
  }
  .detail {
    width: 100%;
  }
}
</style>
