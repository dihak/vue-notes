<template>
  <v-dialog v-model="dialog" persistent max-width="600px">
    <v-card>
      <v-card-title>
        <span class="headline">Edit note</span>
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
        <v-btn color="blue darken-1" text @click="$emit('cancel')">Close</v-btn>
        <v-btn color="blue darken-1" text @click="save()">Save</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
<script>
export default {
  name: 'edit-note-dialog',
  props: ['dialog', 'item'],
  data: () => ({
    title: null,
    content: null,
  }),
  methods: {
    save: function() {
      this.$emit('save', this.note)
    }
  },
  computed: {
    note: function() {
      return {
        title: this.title,
        content: this.content
      }
    }
  },
  watch: {
    item: function() {
      this.title = this.item.title
      this.content = this.item.content
    }
  }
}
</script>
