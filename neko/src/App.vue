<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

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
      <h2>自分だけのオリジナルねこちゃんをつくろう。</h2>

      <img alt="ねこのイラスト" class="image-cat" src="" width="200" height="200" />
      <p v-bind:style="{ display: 'inline-block', backgroundColor: backgroundColor }"></p>

      <p><span v-if="name">なまえは {{ name }} です。</span><span v-else>おなまえを入力してください。</span></p>
      <p><input type="text" name="name" v-model="name"></p>
      
      <input type="range" name="range" v-model="rotate" min="0" step="0.01" max="1">
      <p>{{ rotate }} turn</p>

      <p class="color-picker">カラーピッカー</p>
      <input type="color" name="color" v-model="backgroundColor">
      <p class="color-code">カラーコードを表示</p>
      <p>{{ backgroundColor }}</p>
    </div>
  </main>
</template>

<style scoped>
.logo {
  display: block;
  margin: 0 auto 2rem;
}
input[type="color"] {
  border: none;
  outline: none;
  width: 120px;
  height: 40px;
  cursor: pointer;
}
</style>
