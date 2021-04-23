<template>
  <button class="customselect__button" @click="handleCustomSelectToggle()">
    ⇅
  </button>
  <div
    class="customselect__container"
    v-show="customselect_toggle"
    @click.self="handleCustomSelectToggle()"
  >
    <div class="customselect__menu">
      <div
        class="customselect__options"
        @click="handleOptionSelectLocal('title')"
      >
        Title
      </div>
      <div
        class="customselect__options"
        @click="handleOptionSelectLocal('newest')"
      >
        Newest
      </div>
      <div
        class="customselect__options"
        @click="handleOptionSelectLocal('oldest')"
      >
        Oldest
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CustomSelect",
  props: ["handleOptionSelect"],
  data() {
    return {
      customselect_toggle: false,
    };
  },
  methods: {
    handleCustomSelectToggle() {
      this.customselect_toggle = !this.customselect_toggle;
    },
    handleOptionSelectLocal(sort_by) {
      this.handleCustomSelectToggle();
      this.handleOptionSelect(sort_by);
    },
  },
};
</script>

<style scoped>
.customselect__button {
  min-width: 6vh;
  min-height: 35px;
  height: 6vh;
  border: none;
  outline: none;
  border-radius: 25px;
  color: black;
  background-color: aqua;
  font-size: 1.2em;
  font-weight: 600;
}

.customselect__button:hover {
  cursor: pointer;
  background-color: rgb(0, 163, 163);
  box-shadow: 1px 1px 10px rgb(0, 163, 163);
}

.customselect__container {
  position: absolute;
  top: 0%;
  left: 0%;
  width: 100%;
  height: 100vh;
  background-color: rgba(255, 255, 255, 0);
}

.customselect__menu {
  position: absolute;
  top: 10vh;
  right: 11.8%;
  width: 10%;
  height: 20vh;
  background-color: #111111;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.customselect__options {
  width: 75%;
  height: 4vh;
  color: black;
  background-color: aqua;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 25px;
}

.customselect__options:hover {
  cursor: pointer;
  background-color: rgb(0, 163, 163);
  box-shadow: 1px 1px 10px rgb(0, 163, 163);
}

@media only screen and (max-width: 1250px) {
  .customselect__menu {
    width: 12%;
    right: 10.5%;
  }
}

@media only screen and (max-width: 1200px) {
  .customselect__menu {
    width: 13%;
    right: 8.75%;
  }
}

@media only screen and (max-width: 1150px) {
  .customselect__menu {
    width: 15%;
    right: 6.5%;
  }
}

@media only screen and (max-width: 1100px) {
  .customselect__menu {
    width: 17%;
    right: 5%;
  }
}

@media only screen and (max-width: 1000px) {
  .customselect__menu {
    width: 18%;
    right: 16%;
  }
}

@media only screen and (max-width: 900px) {
  .customselect__menu {
    width: 20%;
    right: 15%;
  }
}

@media only screen and (max-width: 750px) {
  .customselect__menu {
    width: 25%;
    right: 12.5%;
  }
}

@media only screen and (max-width: 600px) {
  .customselect__menu {
    width: 30%;
    right: 9.5%;
  }
}

@media only screen and (max-width: 450px) {
  .customselect__menu {
    width: 35%;
    right: 7.5%;
  }
}
</style>
