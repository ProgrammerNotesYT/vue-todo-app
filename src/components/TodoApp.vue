<template>
  <div class="container" style="max-width: 600px">

    <!-- Heading -->
    <my-heading></my-heading>

    <!-- Input -->
    <my-input ref="myInput" @submitTask="submitTask"></my-input>

    <!-- Task table -->
    <my-table 
      :tasks="tasks"
      @changeStatus="changeStatus"
      @deleteTask="deleteTask"
      @editTask="editTask"
    ></my-table>
    
  </div>
</template>

<script>

import MyHeading from "./my-components/MyHeading.vue";
import MyInput from "./my-components/MyInput.vue";
import MyTable from "./my-components/MyTable.vue";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  components: {
    MyHeading,
    MyInput,
    MyTable
  },

  data() {
    return {
      editedTask: null,
      statuses: ["to-do", "in-progress", "finished"],

      /* Status could be: 'to-do' / 'in-progress' / 'finished' */
      tasks: [
        {
          name: "Steal bananas from the supermarket.",
          status: "to-do",
        },
        {
          name: "Eat 1 kg chocolate in 1 hour.",
          status: "in-progress",
        },
        {
          name: "Create YouTube video.",
          status: "finished",
        },
      ],
    };
  },

  methods: {
    /**
     * Change status of task by index
     */
    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },

    /**
     * Deletes task by index
     */
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    /**
     * Edit task
     */
    editTask(index) {
      this.$refs.myInput.task = this.tasks[index].name;
      this.editedTask = index;
    },

    /**
     * Add / Update task
     */
    submitTask(task) {
      if (task.length === 0) return;

      /* We need to update the task */
      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = task;
        this.editedTask = null;
      } else {
        /* We need to add new task */
        this.tasks.push({
          name: task,
          status: "todo",
        });
      }
    },
  },
};
</script>