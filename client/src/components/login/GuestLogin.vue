<template>
  <div>
    <form class="LoginAsUser">
      <br />
      <br />
      <i class="glyphicon glyphicon-user"></i>
      <input type="text" name="Username" placeholder="Username" v-model="username" />
      <br />
      <br />
      <br />
    </form>
    <button id="loginb" v-on:click="login()">Login</button>
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
  </div>
</template>

<script>
import AuthenticationService from "../../services/AuthenticationService.js";

export default {
  name: "GuestLogin",

  data() {
    return {
      username: ""
    };
  },

  methods: {
    async login() {
      try {
        const response = await AuthenticationService.login({
          username: this.username,
          guest: true
        });
        this.$store.dispatch('setUser', response.data.user)
        this.$store.dispatch('setToken', response.data.token)
        this.$router.push({
          name: "choosearoom"
        });
      } catch (error) {
        alert(error.response.data.error);
      }
    }
  }
};
</script>

<style scoped>
.textfields {
  padding: 5px;
}

input {
  text-align: left;
  padding: 5px 85px 5px 7px;
  height: 40px;
  border: 0;
  background-color: white;
  border-radius: 5px;
}

i {
  color: white;
  margin-right: 8px;
  transform: scale(1.25);
}

#loginb {
  padding: 8px 70px 8px 7px;
  cursor: pointer;
  background-color: white;
  border-radius: 5px;
  border: 0;
  font-weight: bold;
  font-family: "Montserrat", sans-serif;
  text-indent: 78%;
}

#loginb:hover {
  opacity: 0.7;
}
</style>