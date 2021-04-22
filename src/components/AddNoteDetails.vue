<template>
  <div
    class="note__details"
    @click.self="handleNoteAddLocal(note_title, note_data)"
  >
    <div class="note__editor">
      <div class="note__header">
        <input type="text" placeholder="enter title" v-model="note_title" />
        <button @click.self="handleNoteAddLocal(note_title, note_data)">
          ✔
        </button>
      </div>
      <textarea placeholder="enter details" v-model="note_data" />
    </div>
  </div>
</template>

<script>
export default {
  name: "AddNoteDetails",
  props: ["handleNoteAdd"],
  data() {
    return {
      note_title: "",
      note_data: "",
    };
  },
  methods: {
    handleNoteAddLocal(note_title, note_data) {
      this.note_title = "";
      this.note_data = "";
      this.handleNoteAdd(note_title, note_data);
    },
  },
};
</script>

<style scoped>
.note__details {
  position: absolute;
  top: 0;
  width: 100%;
  height: 100vh;
  background-color: rgba(61, 61, 61, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.note__editor {
  width: 40%;
  height: 50vh;
  color: white;
  background-color: white;
  word-wrap: break-word;
}

.note__header {
  padding: 1%;
  width: 100%;
  height: 12%;
  background-color: aqua;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.note__header > input {
  width: 90%;
  height: 100%;
  border: none;
  outline: none;
  background-color: aqua;
  font-size: 1em;
  font-weight: bold;
  text-align: center;
}

.note__header > button {
  background: none;
  border: none;
  outline: none;
  font-size: 1.5em;
}

.note__header > button:hover {
  cursor: pointer;
}

.note__editor > textarea {
  padding: 5%;
  width: 100%;
  height: 90%;
  color: white;
  border: none;
  outline: none;
  background-color: #161616;
  box-sizing: border-box;
  font-size: 1em;
  overflow-y: hidden;
  resize: none;
}

@media only screen and (max-width: 1150px) {
  .note__editor {
    width: 50%;
  }
}

@media only screen and (max-width: 900px) {
  .note__editor {
    width: 60%;
  }
}

@media only screen and (max-width: 750px) {
  .note__editor {
    width: 70%;
  }
}

@media only screen and (max-width: 600px) {
  .note__editor {
    width: 85%;
  }
}
</style>
