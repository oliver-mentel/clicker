<template>
  <div id="wrapper">
    <header>
      <HeaderComponent />
    </header>
    <div id="app">
      <UserNameComponent
        v-on:submitUsername="userNameReceived"
        v-if="!userName"
      />
      <div v-else>
        <ClickerComponent :userName="userName" />
      </div>
    </div>
  </div>
  <footer>
    <FooterComponent />
  </footer>
</template>

<script>
import ClickerComponent from "./components/ClickerComponent.vue";
import FooterComponent from "./components/FooterComponent.vue";
import UserNameComponent from "./components/UserNameComponent.vue";
import HeaderComponent from "./components/HeaderComponent.vue";

export default {
  name: "App",
  components: {
    ClickerComponent,
    FooterComponent,
    UserNameComponent,
    HeaderComponent,
  },
  props: {
    userName: String,
  },
  data() {
    return {
      userName: "",
    };
  },

  methods: {
    userNameReceived(userName) {
      this.userName = userName;
    },
  },
};
</script>

<style>
html,
body {
  height: 100%;
  width: 100%;
  margin: 0;
  /* display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center; */
}
html,
body {
  margin: 0;
  /* background: linear-gradient(
    135deg,
    rgba(51, 120, 255, 1) 0%,
    rgba(148, 66, 254, 1) 100%
  ); */
  background-color: rgb(118, 51, 212);
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 100%;
}

/* place footer always at the bottom with dynamic content */
footer {
  /* position: absolute;
  bottom: 0;
  width: 100%;
  height: auto;
  margin-top: 40px; */

  width: 100%;
  margin-top: 50px;
  height: 100px;
  position: relative;
  clear: both;
}

*/ #wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  /* place all elements evenly  */
  justify-content: space-evenly;
  min-height: 100%;
  height: auto !important;
  height: 100%;
}
#app {
  font-family: "Roboto", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #eee;
  height: auto;
  width: auto;
  /* background: linear-gradient(
    135deg,
    rgba(51, 120, 255, 1) 0%,
    rgba(148, 66, 254, 1) 100%
  );
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat; */
}
</style>
