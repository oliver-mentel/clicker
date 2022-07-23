<template>
  <!-- Header -->
  <div @click="navBackToLandingPage()" class="header-container">
    <h1 class="header">CLICKER</h1>
    <i class="fa-solid fa-arrow-pointer"></i>
  </div>
</template>

<script>
export default {
  name: "HeaderComponent",
  data() {
    return {
      isExit: false,
    };
  },
  methods: {
    navBackToLandingPage() {
      this.$emit("isExit", this.isExit);
    },
  },
};
</script>

<style scoped>
.header-container {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  flex-direction: row;
  flex-wrap: nowrap;
  align-content: center;
  gap: 10px;
}
.header {
  font-family: "Roboto", sans-serif;
  font-weight: 200 !important;
  letter-spacing: -5px;
  font-size: 40px;
  margin: 0px 0px 50px 0px;
  padding-top: 30px;
  cursor: pointer;
}
.fa-arrow-pointer {
  font-size: 20px;
  color: #fff;
  margin-top: -10px;
}
</style>
