<template>
  <div id="app">
    <h1 class="title"> Note App Simple</h1>
    <input type="text" v-model="newNote" placeholder="Add new note" @keyup.enter="addNote" class="input-field">
    <div v-if="editingIndex !== null" class="edit-section">
      <input type="text" v-model="editedNote" @keyup.enter="updateNote" class="edit-input-field">
      <button @click="updateNote" class="update-button">Update</button>
      <button @click="cancelEdit" class="cancel-button">Cancel</button>
    </div>
    <ul class="note-list">
      <li v-for="(note, index) in notes" :key="index" class="note-item">
        <span>{{ note }}</span>
        <div class="button-container">
          <button @click="editNote(index)" class="edit-button">Edit</button>
          <button @click="deleteNote(index)" class="delete-button">Delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      notes: [],
      newNote: '',
      editingIndex: null,
      editedNote: '',
    };
  },
  methods: {
    addNote() {
      if (this.newNote.trim() !== '') {
        this.notes.push(this.newNote.trim());
        this.newNote = '';
      }
    },
    editNote(index) {
      this.editedNote = this.notes[index];
      this.editingIndex = index;
    },
    updateNote() {
      if (this.editedNote.trim() !== '') {
        this.notes[this.editingIndex] = this.editedNote.trim();
        this.editedNote = '';
        this.editingIndex = null;
      }
    },
    cancelEdit() {
      this.editedNote = '';
      this.editingIndex = null;
    },
    deleteNote(index) {
      this.notes.splice(index, 1);
      if (this.editingIndex === index) {
        this.editedNote = '';
        this.editingIndex = null;
      }
    },
  },
};
</script>

<style>
#app {
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-align: center;
}

.title {
  font-size: 24px;
  margin-bottom: 20px;
}

.input-field {
  padding: 10px;
  font-size: 16px;
  border: 2px solid #00e1ff;
  border-radius: 5px;
  margin-bottom: 20px;
}

.edit-section {
  margin-bottom: 20px;
}

.edit-input-field {
  padding: 10px;
  font-size: 16px;
  border: 2px solid #007bff;
  border-radius: 5px;
}

.update-button, .cancel-button {
  padding: 10px 20px;
  margin-left: 10px;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.update-button {
  background-color: #28a745;
  color: white;
}

.cancel-button {
  background-color: #dc3545;
  color: white;
}

.note-list {
  list-style-type: none;
  padding-left: 0;
}

.note-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 0;
  border-bottom: 1px solid #ddd;
}

.button-container {
  display: flex;
  gap: 10px;
}

.edit-button, .delete-button {
  padding: 8px 16px;
  font-size: 14px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.edit-button {
  background-color: #007bff;
  color: white;
}

.delete-button {
  background-color: #dc3545;
  color: white;
}
body{
  background-color: #2fdca5;
}
</style>