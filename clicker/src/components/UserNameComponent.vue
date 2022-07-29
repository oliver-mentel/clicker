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
          maxlength="20"
          required
          :style="isCharacterLimit"
        />
        <!-- Span element which displays when max character length is met -->
        <span v-if="username.length >= 20" class="max-length-warning"
          >Maximum character length is 20</span
        >
        <button
          @click="submitUsername()"
          type="submit"
          :disabled="isDisabled"
          class="submit-btn"
        >
          Submit
        </button>
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
  data() {
    return {
      username: "",
    };
  },
  computed: {
    isDisabled() {
      return this.username.length === 0;
    },
    isCharacterLimit() {
      if (this.username.length >= 20) {
        return "border: 1px solid red; box-shadow: 0px 0px 5px 3px #ff000070; outline: none;";
      }
    },
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
  display: flex;
  justify-content: center;
  align-items: center;
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
  min-width: 330px;
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
.max-length-warning {
  font-size: 12px;
  margin-top: 10px;
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
  text-align: center;
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
