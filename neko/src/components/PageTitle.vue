<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
  <h1>{{ msg }}</h1>
  <h2>じぶんだけのオリジナルねこをつくろう。</h2>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 3.4rem;
  letter-spacing: .05em;
  text-align: center;
  font-family: 'Cherry Bomb One', cursive;
  color: #f5dada;
}

h2 {
  font-size: 1.4rem;
  letter-spacing: .08em;
  text-align: center;
  margin: 0 auto 40px;
  font-family: 'Cherry Bomb One', cursive;
}
@media screen and (max-width: 900px) {
  h1 {
    font-size: 2.4rem;
  }
  h2 {
    font-size: 1.1rem;
  }
}
</style>
