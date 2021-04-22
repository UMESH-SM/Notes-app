<template>
  <div class="home">
    <AppBar
      :handleSearch="handleSearch"
      :handleNoteAddToggle="handleNoteAddToggle"
      :handleSort="handleSort"
    />
    <div class="home__container" v-if="notesCopy.length">
      <Note
        v-for="(note, i) in notesCopy"
        :key="note.id"
        :note="note"
        :handleNoteEdit="handleNoteEdit"
        :search="search"
        :handleNoteDelete="handleNoteDelete"
        :note_color="colors[i % 14]"
      />
    </div>
    <div class="empty__container" v-else>
      <img
        src="https://i.pinimg.com/originals/ae/8a/c2/ae8ac2fa217d23aadcc913989fcc34a2.png"
        alt="You have no notes to display."
      />
    </div>
    <AddNoteDetails v-show="note_add_toggle" :handleNoteAdd="handleNoteAdd" />
  </div>
</template>

<script>
import AppBar from "./AppBar.vue";
import Note from "./Note.vue";
import AddNoteDetails from "./AddNoteDetails";
import { db, fire } from "../../firebase_config";

export default {
  name: "Home",
  components: {
    AppBar,
    Note,
    AddNoteDetails,
  },
  data() {
    return {
      notes: [],
      notesCopy: [],
      search: "",
      note_add_toggle: false,
      colors: [
        "#8EE4AF",
        "#DAAD86",
        "#C38D9E",
        "#E27D60",
        "#26ABBA",
        "#88C44C",
        "#CAFAFE",
        "#ADADAD",
        "#E7717D",
        "#ffff80",
        "#adad85",
        "#C5C6C7",
        "#FFCB9A",
        "#adadeb",
      ],
    };
  },
  mounted() {
    const user = fire.auth().currentUser;
    db.collection(user.uid)
      .doc("notes")
      .get()
      .then((doc) => {
        if (doc.exists) {
          const notes_data = doc.data();
          this.notes = notes_data.notesList;
        }
      })
      .catch((error) => {
        console.log("Error fetching data in Home : " + error);
      });
  },
  watch: {
    notes: {
      handler: function(newValue) {
        this.notesCopy = newValue;
        const user = fire.auth().currentUser;
        db.collection(user.uid)
          .doc("notes")
          .set({
            notesList: this.notes,
          })
          .catch((error) => {
            console.log("Error updating data in Home : " + error);
          });
      },
      deep: true,
    },
  },
  methods: {
    handleNoteAddToggle() {
      this.note_add_toggle = !this.note_add_toggle;
    },
    handleNoteAdd(note_title, note_data) {
      if (note_title !== "" || note_data !== "") {
        this.notes.unshift({
          id: new Date().getMilliseconds(),
          title: note_title,
          data: note_data,
        });
      }
      this.handleNoteAddToggle();
    },
    handleNoteEdit(id, note_title, note_data) {
      this.notes = this.notes.map((note) => {
        if (note.id === id) {
          return {
            id: note.id,
            title: note_title,
            data: note_data,
          };
        } else return note;
      });
    },
    handleSearch(search) {
      this.search = search;
      this.notesCopy = this.notes.filter(
        (note) =>
          note.title.toLowerCase().includes(search.toLowerCase()) ||
          note.data.toLowerCase().includes(search.toLowerCase())
      );
    },
    handleNoteDelete(id) {
      this.notes = this.notes.filter((note) => note.id !== id);
    },
    handleSort(sort_by) {
      if (sort_by === "title") {
        this.notesCopy.sort((a, b) => {
          if (a.title.toLowerCase() < b.title.toLowerCase()) {
            return -1;
          }
          return 1;
        });
      } else if (sort_by === "newest") {
        this.notesCopy.sort((a, b) => b.id - a.id);
      } else if (sort_by === "oldest") {
        this.notesCopy.sort((a, b) => a.id - b.id);
      }
    },
  },
};
</script>

<style scoped>
.home {
  min-height: 100vh;
}

.home__container {
  box-sizing: border-box;
  width: 100%;
  min-height: 100vh;
  height: fit-content;
  padding: 20vh 5% 5% 5%;
  display: flex;
  align-items: flex-start;
  justify-content: space-around;
  flex-wrap: wrap;
  background-color: #1f1f1f;
}

.empty__container {
  padding: 5%;
  min-width: 300px;
  min-height: 450px;
  width: 100%;
  height: 100vh;
  box-sizing: border-box;
  background-color: #1f1f1f;
  position: relative;
  z-index: -1;
}

.empty__container > img {
  margin-top: 8vh;
  height: 70vh;
  filter: brightness(15%);
  border-radius: 50%;
}

@media only screen and (max-width: 750px) {
  .empty__container > img {
    margin-top: 30vh;
    height: 30vh;
  }
}

@media only screen and (max-width: 600px) {
  .empty__container > img {
    margin-top: 30vh;
    height: 30vh;
  }
}

/* @media only screen and (max-width: 900px) {
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
} */
</style>
