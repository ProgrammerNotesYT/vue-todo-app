<template>
  <div class="d-flex mt-5">
    <input
      type="text"
      v-model="task"
      placeholder="Enter task"
      class="w-100 form-control"
    />
    <button class="btn btn-warning rounded-0" @click="submitTask">
      SUBMIT
    </button>
  </div>
</template>

<script>
export default {
  name: "MyInput",

  data() {
    return {
      task: "",
    };
  },

  methods: {
    submitTask() {
      this.$emit("submitTask", this.task);
      this.task = "";
    },
  },
};
</script>