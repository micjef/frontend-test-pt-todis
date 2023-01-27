<template>
  <v-dialog
    :value="true"
    persistent
    max-width="80vw"
  >
    <v-card>
      <v-card-title class="text-h5">
        Edit task
      </v-card-title>
      <v-card-text>Title</v-card-text>
      <v-text-field 
        v-model="taskTitle"
        @keyup.enter="saveTask"
        class="ma-6"
      />
      <v-card-text>Description</v-card-text>
      <v-text-field 
        v-model="taskDescription"
        @keyup.enter="saveTask"
        class="ma-6"
      />
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
          @click="$emit('close')"
          text
        >
          Cancel
        </v-btn>
        <v-btn
          @click="saveTask"
          :disabled="!taskTitle.length || taskTitle === task.title && taskDescription === task.description"
          text
        >
          Save new
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: 'todo-edit',
  props: ['task'],
  data() {
    return {
      taskTitle: '',
      taskDescription: ''
    }
  },
  mounted() {
    this.taskTitle = this.task.title
    this.taskDescription = this.task.description
  },
  methods: {
    saveTask() {
      const payload = {
        id: this.task.id,
        title: this.taskTitle,
        description: this.taskDescription
      }
      this.$store.dispatch('updateTaskTitle', payload)
      this.$emit('close')
      this.$vuetify.goTo(0, { duration: 0 })
    }
  }
}
</script>