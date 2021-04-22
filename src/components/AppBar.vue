<template>
  <div class="appbar">
    <div class="appbar__title">Notes App</div>
    <div class="appbar__search">
      <input
        type="text"
        placeholder="search"
        @input="handleSearch($event.target.value)"
      />
    </div>
    <div class="appbar__buttons">
      <button @click="handleNoteAddToggle()">📋</button>
      <CustomSelect :handleOptionSelect="handleSort" />
      <button @click="handleLogout()">
        👋
      </button>
    </div>
  </div>
</template>

<script>
import { fire } from "../../firebase_config";
import CustomSelect from "./CustomSelect.vue";

export default {
  name: "AppBar",
  components: { CustomSelect },
  props: ["handleSearch", "handleNoteAddToggle", "handleSort"],
  data() {
    return {
      sort_toggle: false,
    };
  },
  methods: {
    handleLogout() {
      const res = confirm("Are you sure you want to Logout?");
      if (res) {
        fire.auth().signOut();
        console.log("SignOut successful.");
      }
    },
  },
};
</script>

<style scoped>
.appbar {
  width: 100%;
  min-height: 50px;
  height: 10vh;
  position: fixed;
  background-color: #111111;
  display: flex;
  align-items: center;
  justify-content: space-around;
}

.appbar__title {
  flex: 1;
  color: aqua;
  font-family: "RocknRoll One", sans-serif;
  font-size: 1.3em;
}

.appbar__title:hover {
  cursor: pointer;
  color: rgb(0, 163, 163);
}

.appbar__search {
  flex: 1;
  min-height: 25px;
  height: 5vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.appbar__search > input {
  width: 50%;
  height: 100%;
  padding: 0% 10%;
  border: 3px solid #c4cdd1;
  outline: none;
  border-radius: 10px;
  color: black;
  font-size: 1em;
  font-weight: 500;
  background-color: #c4cdd1;
}

.appbar__search > input:focus-visible {
  background-color: #dce9ee;
  border: 3px solid #3c8dbc;
}

.appbar__buttons {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: space-around;
}

.appbar__buttons > button {
  min-width: 6vh;
  min-height: 35px;
  height: 6vh;
  border: none;
  outline: none;
  border-radius: 25px;
  color: black;
  background-color: aqua;
  font-size: 1.3em;
  font-weight: 500;
}

.appbar__buttons > button:hover {
  cursor: pointer;
  background-color: rgb(0, 163, 163);
}

@media only screen and (max-width: 1200px) {
  .appbar__search {
    flex: 1.25;
  }
}

@media only screen and (max-width: 1150px) {
  .appbar__search {
    flex: 1.5;
  }
}

@media only screen and (max-width: 1100px) {
  .appbar__search {
    flex: 1.75;
  }
}

@media only screen and (max-width: 1000px) {
  .appbar__search {
    flex: 2;
  }
}

@media only screen and (max-width: 1000px) {
  .appbar__title {
    display: none;
  }

  .appbar__search {
    flex: 1;
  }

  .appbar__buttons {
    flex: 1;
  }
}
</style>
