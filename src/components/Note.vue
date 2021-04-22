<template>
  <div class="note" @click="handleToggle()" :style="cssVars">
    <div class="note__title">{{ note.title }}</div>
    <div class="note__data">{{ note.data }}</div>
  </div>
  <EditNoteDetails
    v-show="note_edit_toggle"
    :note_title_prop="note.title"
    :note_data_prop="note.data"
    :handleNoteEditRequest="handleNoteEditRequest"
    :handleNoteDeleteRequest="handleNoteDeleteRequest"
  />
</template>

<script>
import EditNoteDetails from "./EditNoteDetails.vue";

export default {
  name: "Note",
  components: { EditNoteDetails },
  props: ["note", "handleNoteEdit", "search", "handleNoteDelete", "note_color"],
  data() {
    return {
      note_edit_toggle: false,
    };
  },
  methods: {
    handleToggle() {
      this.note_edit_toggle = !this.note_edit_toggle;
    },
    handleNoteEditRequest(note_title, note_data) {
      if (note_title !== this.note.title || note_data !== this.note.data) {
        this.handleNoteEdit(this.note.id, note_title, note_data);
      }
      this.handleToggle();
    },
    handleNoteDeleteRequest() {
      this.handleNoteDelete(this.note.id);
    },
  },
  computed: {
    cssVars() {
      return {
        "--bg-color": this.note_color,
      };
    },
  },
};
</script>

<style scoped>
.note {
  width: 11%;
  height: 20vh;
  background-color: var(--bg-color);
  padding: 1%;
  word-wrap: break-word;
  cursor: pointer;
  margin-bottom: 3%;
  overflow-y: scroll;
}

.note::-webkit-scrollbar {
  display: none;
}

.note::-webkit-scrollbar {
  display: none;
}

@-moz-document url-prefix() {
  .note {
    overflow-y: hidden;
  }
}

@supports (-ms-ime-align: auto) {
  .note {
    overflow-y: hidden;
  }
}

.note__title {
  font-size: 1em;
  font-weight: bold;
}

.note__data {
  margin-top: 10%;
}

@media only screen and (max-width: 1250px) {
  .note {
    width: 13%;
  }
}

@media only screen and (max-width: 1200px) {
  .note {
    width: 15%;
  }
}

@media only screen and (max-width: 1100px) {
  .note {
    width: 20%;
  }
}

@media only screen and (max-width: 900px) {
  .note {
    width: 25%;
  }
}

@media only screen and (max-width: 750px) {
  .note {
    width: 35%;
  }
}

@media only screen and (max-width: 600px) {
  .note {
    width: 70%;
    height: 30vh;
    margin-bottom: 5%;
  }
}
</style>
