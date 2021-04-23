<template>
  <div
    class="note__details"
    @click.self="handleNoteEditRequest(note_title, note_data)"
  >
    <div class="note__editor">
      <div class="note__header">
        <button class="note__delete" @click.self="handleNoteDeleteConfirm()">
          ⛔
        </button>
        <input type="text" v-model="note_title" placeholder="enter title" />
        <button
          class="note__save"
          @click.self="handleNoteEditRequest(note_title, note_data)"
        >
          👍
        </button>
      </div>
      <textarea v-model="note_data" placeholder="enter details" />
    </div>
  </div>
</template>

<script>
export default {
  name: "EditNoteDetails",
  props: [
    "note_title_prop",
    "note_data_prop",
    "handleNoteEditRequest",
    "handleNoteDeleteRequest",
  ],
  data() {
    return {
      note_title: this.note_title_prop,
      note_data: this.note_data_prop,
    };
  },
  methods: {
    handleNoteDeleteConfirm() {
      let res = confirm("Are you sure you want to delete this Note?");
      if (res) {
        this.handleNoteDeleteRequest();
      }
    },
  },
};
</script>

<style scoped>
.note__details {
  position: fixed;
  top: 50%;
  left: 50%;
  width: 100%;
  height: 100vh;
  transform: translate(-50%, -50%);
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
  font-size: 1.3em;
}

.note__header > button:first-child {
  font-size: 1em;
}

.note__header > button:hover {
  cursor: pointer;
  transform: scale(1.08);
  transition: 0.6s ease;
}

/* .note__delete {
  color: red;
} */

/* .note__save {
  font-size: 1.2em;
} */

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
