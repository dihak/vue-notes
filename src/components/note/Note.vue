<template>
    <v-col cols="12" sm="3">
        <v-card>
            <v-card-title>
              {{note.title}}
            </v-card-title>
            <v-card-text>
              {{note.content}}
            </v-card-text>
            <v-card-actions>
                <v-btn text @click="$emit('edit')">EDIT</v-btn>
                <v-spacer></v-spacer>
                <v-btn icon color="red" @click="$emit('delete')"><v-icon>mdi-delete-outline</v-icon></v-btn>
            </v-card-actions>
        </v-card>
    </v-col>
</template>
<script>
export default {
  name: 'note',
  props: ['note']
}
</script>
