<template>
  <div class="login">
    <h1>This is a Login page</h1>
    <h5 v-if="!isLoggedIn">Click login Button to Login</h5>
    <h5 v-else>Click login Button to Logout</h5>

    <div class="container-fluid">
      <div class="row">
        <button
          v-if="!isLoggedIn"
          id="loginBtn"
          class="btn btn-success"
          @click="login()"
        >
          Login
        </button>
        <button v-else id="logoutBtn" class="btn btn-danger" @click="logout()">
          Logout
        </button>
      </div>
    </div>
    <br />
    <div>
      <p>
        Login Status:
        <span v-if="isLoggedIn" class="text-success">Logged In</span>
        <span v-else class="text-danger">Not Logged In</span>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "LoginView",
  data() {
    return {
      isLoggedIn: false,
    };
  },
  methods: {
    login() {
      localStorage.setItem("token", "loginUser123");
      this.checkLoginStatus();
      alert("login successfully!!");
    },
    logout() {
      localStorage.removeItem("token");
      this.checkLoginStatus();
      alert("logout successfully!!");
    },
    checkLoginStatus() {
      this.isLoggedIn = localStorage.getItem("token") !== null;
    },
  },
  mounted() {
    this.checkLoginStatus();
  },
};
</script>
