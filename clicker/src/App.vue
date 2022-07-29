<template>
  <div id="wrapper">
    <HeaderComponent v-on:isExit="navigateToLandingPage" />
    <div>
      <UserNameComponent
        v-on:submitUsername="userNameReceived"
        v-if="!userName"
      />
      <div v-else>
        <ClickerComponent :userName="userName" />
      </div>
    </div>
    <FooterComponent />
  </div>
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
      isExit: false,
    };
  },

  methods: {
    userNameReceived(userName) {
      this.userName = userName;
    },
    navigateToLandingPage() {
      this.isExit = true;
      this.userNameReceived("");
    },
  },
};
</script>

<style>
body,
html {
  height: 100%;
  width: 100%;
  margin: 0;
  background: linear-gradient(
    135deg,
    rgba(51, 120, 255, 1) 0%,
    rgba(148, 66, 254, 1) 100%
  );
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
  touch-action: manipulation;
}

/* place footer always at the bottom with dynamic content */
footer {
  width: 100%;
  margin-top: 50px;
  height: 100px;
  position: relative;
  clear: both;
}

#wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  height: 100%;
}
#app {
  font-family: "Roboto", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #eee;
  height: 100%;
  width: auto;
}
.click-btn,
.reset-btn,
.submit-btn {
  position: relative;
  padding: 10px 30px;
  margin: 30px;
  width: fit-content;
  border: 0px solid grey;
  border-radius: 20px;
  background-color: #fbab7e;
  overflow: hidden;
  font-size: 20px;
  color: #fff;
  cursor: pointer;
  transition: 0.2s all;
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Old versions of Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none; /* Non-prefixed version, currently
  supported by Chrome, Edge, Opera and Firefox */
}

.click-btn {
  font-size: 30px;
}

@media (max-width: 1100px) {
  .click-btn {
    width: 30vw;
    height: 10vh;
    padding: 0px;
    font-size: 5vw;
  }
}

.click-btn:active {
  transform: scale(0.8);
  /* Scaling button to 0.98 to its original size */
  box-shadow: 0px 5px 17px 4px rgb(0 0 0 / 24%);
  /* Lowering
 the shadow */
}
.click-btn:hover,
.reset-btn:hover,
.submit-btn:hover {
  background-color: #f89156;
  transform: scale(0.98);
}

.reset-btn:disabled,
.submit-btn:disabled {
  background-color: #fbac7ea6;
  cursor: auto;
}
</style>
