<template>
  <v-container fluid>
    <v-row >
      <v-col v-for="(task, index) in tasks" :key="index" cols="6">
        <v-card class="bg-cyan-darken-2">
          <v-card-title>{{ task.title }}</v-card-title>
          <v-card-subtitle>{{ task.subtitle }}</v-card-subtitle>
          <v-card-text>{{ task.text }}</v-card-text>
          <v-card-actions>
            <v-checkbox
              v-model="ex4"
              label="Done"
              color="indigo"
              value="indigo"
              hide-details
            ></v-checkbox>
            <v-btn @click="removeTask(index)" icon active>
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  
    <v-col cols="auto" align="center" justify="center">
      <v-btn size="x-large" @click="showAddTaskDialog">Add Task</v-btn>
    </v-col>

    <!-- Add Task Dialog -->
    <v-dialog v-model="addTaskDialog" max-width="500px">
      <v-card>
        <v-card-title align="center">Add New Task</v-card-title>
        <v-card-text>
          <v-text-field v-model="newTaskTitle" label="Task Title"></v-text-field>
          <v-textarea v-model="newTaskText" label="Task Details"></v-textarea>
          <v-alert class="bg-red-darken-2" v-model="alert" text="Make sure both of the fields are not empty"></v-alert>
        </v-card-text>
        <v-card-actions>
          <v-btn @click="cancelAddTask">Cancel</v-btn>
          <v-btn @click="saveNewTask" color="primary">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

</v-container>
</template>

<script>
export default {
  name: 'HelloWorld',

  data() {
    return {
      ex4: ['indigo'],
      tasks: [
        {
          title: 'Card title',
          subtitle: this.getFormattedDate(),
          text: '...'
        }
      ],
      alert:false,
      addTaskDialog: false,
      newTaskTitle: '',
      newTaskText: ''
    };
  },
  methods: {
    showAddTaskDialog() {
      this.addTaskDialog = true;
    },
    cancelAddTask() {
      this.addTaskDialog = false;
      this.alert=false;
      this.newTaskTitle = '';
      this.newTaskText = '';
    },
    saveNewTask() {
      if (this.newTaskTitle.trim() !== '' && this.newTaskText.trim() !== '') {
        this.tasks.push({
          title: this.newTaskTitle,
          subtitle: this.getFormattedDate(),
          text: this.newTaskText
        });
        this.addTaskDialog = false;
        this.newTaskTitle = '';
        this.newTaskText = '';
        this.alert=false; 
      }else{
        this.alert=true;
      }
    },
    getFormattedDate() {
      const currentDate = new Date();
      return currentDate.toLocaleString();
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>