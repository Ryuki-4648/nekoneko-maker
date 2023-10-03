<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import { ref } from 'vue';

const name = ref('');
const rotate = ref(0);
const backgroundColor = ref('#fafafa');
</script>
<!-- script setup コンポーネントのロジックを設定 -->

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
    <div>
      <h1>ねこねこメーカー</h1>
      <h2>自分だけのオリジナルねこをつくろう。</h2>

      <img alt="ねこのイラスト" class="image-cat" src="" width="200" height="200" />
      <p v-bind:style="{ display: 'inline-block', backgroundColor: backgroundColor }"></p>

      <p><span v-if="name">おなまえは {{ name }} です。</span><span v-else>おなまえを入力してください。</span></p>
      <p><input type="text" v-model="name" class="input-name"></p>
      
      <input type="range" name="range" v-model="rotate" min="0" step="0.01" max="1">
      <p>{{ rotate }} turn</p>

      <p class="color-picker">カラーピッカー</p>
      <input type="color" name="color" v-model="backgroundColor">
      <p class="color-code">カラーコード: {{ backgroundColor }}</p>
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
.logo {
  display: block;
  margin: 0 auto 2rem;
}
.input-name {
  border: 1px solid #dadada;
  height: 36px;
  width: 200px;
  padding: 2px 2px 2px 6px;
  font-size: 14px;
}
.image-cat {
  margin: 0 auto 40px;
}
input[type="color"] {
  border: none;
  outline: none;
  width: 120px;
  height: 40px;
  cursor: pointer;
}
</style>
