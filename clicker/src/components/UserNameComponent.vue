<template>
  <!-- Username Form with Submit Button -->
  <div class="username-form-container">
    <div class="items">
      <form @submit.prevent="submitUsername">
        <input
          type="text"
          name="username"
          v-model="username"
          placeholder="Enter Your Name"
          required
        />
        <button @click="submitUsername()" type="submit">Submit</button>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  name: "UserNameComponent",
  props: {
    userName: String,
  },
  methods: {
    submitUsername() {
      this.$emit("submitUsername", this.username);
    },
  },
};
</script>
<style scoped>
/* Place form field in center of page */
.username-form-container {
  /* position: absolute;
  width: auto;
  height: auto; */
  /* top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); */
}

.items {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 500px;
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.1),
    rgba(255, 255, 255, 0)
  );
  -webkit-backdrop-filter: blur(20px);
  box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
  border: 1px solid rgba(255, 255, 255, 0.18);
  border-radius: 32px;
}
input {
  width: 200px;
  height: 40px;
  border-radius: 20px;
  border: 1px solid #fff;
  padding: 0 10px;
  margin-top: 30px;
  font-size: 1.2rem;
  font-weight: bold;
  color: #fff;
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.1),
    rgba(255, 255, 255, 0)
  );
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.18);
}
button {
  position: relative;
  padding: 10px 30px;
  margin: 30px;
  border: 0px solid grey;
  border-radius: 20px;
  background-color: #fbab7e;
  overflow: hidden;
  font-size: 20px;
  color: #fff;
  cursor: pointer;
}
::placeholder {
  /* Chrome, Firefox, Opera, Safari 10.1+ */
  color: rgb(181, 181, 181);
  opacity: 1; /* Firefox */
  text-align: center;
}
</style>
