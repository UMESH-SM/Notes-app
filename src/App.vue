<template>
  <Home v-if="signed_in" />
  <SignIn v-else />
</template>

<script>
import { fire } from "../firebase_config";
import Home from "./components/Home.vue";
import SignIn from "./components/SignIn.vue";

export default {
  name: "App",
  components: {
    Home,
    SignIn,
  },
  data() {
    return {
      signed_in: false,
    };
  },
  created() {
    fire.auth().onAuthStateChanged((user) => {
      if (user) {
        this.signed_in = true;
      } else {
        this.signed_in = false;
      }
    });
  },
};
</script>

<style>
* {
  margin: 0;
  font-family: "Ubuntu", sans-serif;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-tap-highlight-color: rgba(255, 255, 255, 0);
  text-align: center;
  color: #2c3e50;
  min-width: 300px;
  min-height: 450px;
}
</style>
