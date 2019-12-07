<template>
  <v-dialog v-model="dialog" persistent max-width="600px">
    <template v-slot:activator="{ on }">
      <v-btn bottom color="pink" dark fab fixed right v-on="on">
        <v-icon>mdi-plus</v-icon>
      </v-btn>
    </template>
    <v-card>
      <v-card-title>
        <span class="headline">New note</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12">
              <v-text-field label="Title*" required outlined v-model="title"></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-textarea label="Note" outlined v-model="content"></v-textarea>
            </v-col>
          </v-row>
        </v-container>
        <small>*indicates required field</small>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="blue darken-1" text @click="dialog = false">Close</v-btn>
        <v-btn color="blue darken-1" text @click="add()">Add</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
<script>
export default {
  name: 'add-note-dialog',
  data: () => ({
    title: null,
    content: null,
    dialog: false
  }),
  methods: {
    add: function() {
      this.$emit('add', this.note)
      this.dialog = false
      this.title = this.content = null
    }
  },
  computed: {
    note: function() {
      return {
        title: this.title,
        content: this.content
      }
    }
  }
}
</script>
