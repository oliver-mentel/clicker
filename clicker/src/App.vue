<template>
  <div id="app">
    <ClickerComponent msg="Welcome to Your Vue.js App" />
    <FooterComponent />
  </div>
</template>

<script>
import ClickerComponent from "./components/ClickerComponent.vue";
import FooterComponent from "./components/FooterComponent.vue";

export default {
  name: "App",
  components: {
    ClickerComponent,
    FooterComponent,
  },
};
</script>

<style>
html {
  height: auto;
  width: 100%;
  background: #db6b6b;
  background: rgb(51, 120, 255);
  background: linear-gradient(
    135deg,
    rgba(51, 120, 255, 1) 0%,
    rgba(148, 66, 254, 1) 100%
  );
  /* margin-bottom: 10px; */
}
body {
  margin-bottom: 0px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin: 0 auto; */
  /* margin-bottom: 40px; */
  color: #eee;
}
</style>

<!-- <script setup>
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
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style> -->
