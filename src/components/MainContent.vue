<template>
  <v-content>
    <v-container fluid>
        <v-row>
          <note v-for="(item, index) in notesList" v-bind:key="index" v-bind:note="item" v-on:delete="deleteNote(index)" v-on:edit="editNote(index)"/>
        </v-row>
    </v-container>
    <add-note-dialog v-on:add="addNote($event)"/>
    <edit-note-dialog v-on:save="saveEditedNote($event)" v-bind:item="currentNote" v-bind:dialog="editDialog" v-on:cancel="editDialog = currentNote = false"/>
  </v-content>
</template>

<script>
import Note from '@/components/note/Note.vue'
import AddNoteDialog from '@/components/note/AddNoteDialog.vue'
import EditNoteDialog from '@/components/note/EditNoteDialog.vue'
export default {
  name: 'main-content',
  components: {
    Note,
    AddNoteDialog,
    EditNoteDialog
  },
  data: () => ({
    notesList: [],
    currentNote: null,
    editDialog: false
  }),
  mounted: function() {
    if (localStorage.getItem('notes')) {
      try {
        this.notesList = JSON.parse(localStorage.getItem('notes'))
      } catch (e) {
        localStorage.removeItem('notes')
      }
    }
  },
  methods: {
    addNote: function(item) {
      this.notesList.push({
        title: item.title,
        content: item.content
      })
      this.saveNote()
    },
    editNote: function(index) {
      this.currentNote = this.notesList[index]
      this.editDialog = true
    },
    saveEditedNote: function(item) {
      this.currentNote.title = item.title
      this.currentNote.content = item.content
      this.editDialog = false
      this.saveNote()
    },
    deleteNote: function(index) {
      this.notesList.splice(index, 1);
      this.saveNote()
    },
    saveNote: function() {
      localStorage.setItem('notes', JSON.stringify(this.notesList))
    }
  }
}
</script>
