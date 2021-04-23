<template>
  <div class="signin">
    <h2 class="signin__title">{{ has_account ? "SignIn" : "SignUp" }}</h2>
    <form
      class="signin__form"
      @submit.prevent="has_account ? handleSignIn() : handleSignUp()"
    >
      <div class="signin__inputs">
        <label>Email</label>
        <input
          type="text"
          autofocus
          required
          v-model="email"
          @input="clearErrors()"
        />
      </div>
      <div class="signin__inputs">
        <label>Password</label>
        <input
          type="password"
          required
          v-model="password"
          @input="clearErrors()"
        />
      </div>
      <div class="signin__error" v-show="error">
        {{ error }}
      </div>
      <button type="submit">{{ has_account ? "Login" : "Register" }}</button>
    </form>
    <p class="signin__signup__link">
      <span @click="hasAccountToggle()">{{
        has_account ? "New here? SignUp" : "Have an account? SignIn"
      }}</span>
    </p>
    <div class="signin__loader__container" v-show="loading">
      <span class="signin__loader"></span>
    </div>
  </div>
</template>

<script>
import { fire } from "../../firebase_config";
import { db } from "../../firebase_config";

export default {
  name: "SignIn",
  data() {
    return {
      email: "",
      password: "",
      has_account: true,
      error: "",
      loading: false,
    };
  },
  methods: {
    hasAccountToggle() {
      this.clearErrors();
      this.email = "";
      this.password = "";
      this.has_account = !this.has_account;
    },
    clearErrors() {
      this.error = "";
    },
    handleSignIn() {
      this.loading = true;
      fire
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then(() => {
          console.log("SignIn successful.");
        })
        .catch((error) => {
          this.error = error.message;
        });
    },
    handleSignUp() {
      this.loading = true;
      fire
        .auth()
        .createUserWithEmailAndPassword(this.email, this.password)
        .then((userCredential) => {
          db.collection(userCredential.user.uid)
            .doc("notes")
            .set({
              notesList: [],
            })
            .then(() => {
              console.log("SignUp successful.");
            });
        })
        .catch((error) => {
          this.error = error.message;
        });
    },
  },
};
</script>

<style scoped>
.signin {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  background-color: #1f1f1f;
}

.signin__title {
  margin-top: 13vh;
  color: white;
}

.signin__form {
  margin-top: 5vh;
  padding: 1%;
  width: 30%;
  height: 40vh;
  border-radius: 25px;
  background-color: #111313;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.signin__inputs {
  display: flex;
  flex-direction: column;
}

.signin__inputs > label {
  font-weight: bold;
  color: aqua;
}

.signin__inputs > input {
  padding: 1% 2%;
  border: 3px solid #c4cdd1;
  border-radius: 10px;
  outline: none;
  margin: 2% 10%;
  font-size: 1em;
  font-weight: 500;
  text-align: center;
  color: black;
  background-color: #c4cdd1;
}

.signin__inputs > input:focus-visible {
  background-color: #dce9ee;
  border: 3px solid aqua;
}

.signin__form > button {
  padding: 2%;
  margin: 2% 30%;
  border: none;
  border-radius: 10px;
  outline: none;
  background-color: #f0ad4e;
  font-weight: 500;
  font-size: 1em;
}

.signin__form > button:hover {
  background-color: #db932d;
  cursor: pointer;
  box-shadow: 1px 1px 10px #db932d;
}

.signin__signup__link {
  margin-top: 2vh;
  width: 30%;
  text-align: end;
}

.signin__signup__link > span {
  color: #337ab7;
  font-size: 0.95em;
}

.signin__signup__link > span:hover {
  color: #3c8dbc;
  cursor: pointer;
}

.signin__error {
  color: red;
}

.signin__loader__container {
  position: absolute;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  margin-top: 35vh;
}

.signin__loader {
  position: absolute;
  border: 5px solid #f3f3f3;
  border-radius: 50%;
  border-top: 5px solid #db932d;
  width: 25px;
  height: 25px;
  -webkit-animation: spin 0.8s linear infinite; /* Safari */
  animation: spin 0.8s linear infinite;
}

@-webkit-keyframes spin {
  0% {
    -webkit-transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
  }
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@media only screen and (max-width: 1150px) {
  .signin__form {
    width: 40%;
  }
  .signin__signup__link {
    width: 40%;
  }
}

@media only screen and (max-width: 900px) {
  .signin__form {
    width: 50%;
  }
  .signin__signup__link {
    width: 50%;
  }
}

@media only screen and (max-width: 750px) {
  .signin__form {
    width: 60%;
  }
  .signin__signup__link {
    width: 60%;
  }
}

@media only screen and (max-width: 600px) {
  .signin__form {
    width: 75%;
  }
  .signin__signup__link {
    width: 75%;
  }
}
</style>
