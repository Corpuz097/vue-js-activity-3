<template>
  <div class="home">
    <div class="container">
      <div class="imageContainer">
        <img alt="Vue logo" src="../assets/logo.png" />
      </div>
      <div class="titleContainer">
        <h1>Welcome to the Cart</h1>
        <h4 v-if="!isLoggedIn">(Access the Login Page to Login)</h4>
        <h4 v-else>(Access the Login Page to Logout)</h4>
      </div>
    </div>
    <LoginView hidden />
    <HelloWorld :isLoggedIn="isLoggedIn" />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import LoginView from "@/views/LoginView.vue";

export default {
  name: "HomeView",
  components: {
    HelloWorld,
    LoginView,
  },
  data() {
    return {
      isLoggedIn: false,
    };
  },
  methods: {
    checkLoginStatus() {
      this.isLoggedIn = localStorage.getItem("token") !== null;
    },
  },
  mounted() {
    this.checkLoginStatus();
  },
};
</script>

<style>
.container {
  display: flex;
  text-align: center;
}

.imageContainer,
.titleContainer {
  flex: 1;
}

.imageContainer img {
  width: 80px; /* Set the width of the image to 40px */
  height: auto; /* Maintain aspect ratio */
}

.imageContainer {
  margin-right: 20px; /* Adjust margin as needed */
  text-align: right;
}

.titleContainer {
  text-align: left;
  padding-right: 28%;
}
</style>
