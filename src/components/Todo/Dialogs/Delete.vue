<template>
  <v-dialog
    :value="true"
    persistent
    max-width="290"
  >
    <v-card>
      <v-card-title class="text-h5">
        Delete task?
      </v-card-title>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
          @click="$emit('close')"
          text
        >
          No
        </v-btn>
        <v-btn
          @click="$store.dispatch('deleteTask', task.id)"
          text
        >
          Yes
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: 'todo-delete',
  props: ['task']
}
</script>