<template>
  <div id="app">
    <div class="content" v-if="endorseHorses">
      <EndorseHorse v-for="endorse in endorseHorses[0].body" v-bind="(endorse as any)"></EndorseHorse>
    </div>
  </div>
</template>

<script lang="ts" setup>
const { data: endorseHorses } = await useAsyncData('endorseHorses', () => queryContent('/endorse_test').find())
import { computed } from 'vue'
const categories = computed(() => {
  return [
    "All categories",
    ...new Set(endorseHorses[0].body.map(t => t.category).sort())
  ];
})
</script>

<style lang="scss">
$break-small: 765px;

body {
  margin: 0;
  overflow: scroll;
  overflow-x: hidden;
}

* {
  box-sizing: border-box;
}

#app {
  max-width: 960px;
  margin: 0 auto;
  padding: 0px 40px;
  font-family: sans-serif;
  text-align: center;
  font-size: 16px;
  min-height: 100vh;
  display: flex;
  flex-direction: column;

  @media screen and (max-width: $break-small) {
    padding: 0 5%;
  }
}

.content {
  flex-grow: 1;
}

h1,
h2,
h3,
h4,
h5 {
  font-family: 'Raleway', sans-serif;
}

h3 {
  letter-spacing: .06em;
}

.footer-bar {
  background-image: url('./assets/baby.png');
  height: 48px;
  background-size: contain;
  background-repeat: no-repeat;
  width: 100%;
  background-position: center;
  margin-top: 100px;
  transform: translateY(100%);
  transition: transform 0.5s;
  overflow: hidden;

  &.goodBabyShowing {
    transform: translateY(0%);
  }
}
</style>
