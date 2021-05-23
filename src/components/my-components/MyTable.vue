<template>
  <table class="table table-bordered mt-5">
    <thead>
      <tr>
        <th scope="col">Task</th>
        <th scope="col" style="width: 120px">Status</th>
        <th scope="col" class="text-center">#</th>
        <th scope="col" class="text-center">#</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(task, index) in tasks" :key="index">
        <td>
          <span :class="{ 'line-through': task.status === 'finished' }">
            {{ task.name }}
          </span>
        </td>
        <td>
          <span
            class="pointer noselect"
            @click="$emit('changeStatus', index)"
            :class="{
              'text-danger': task.status === 'to-do',
              'text-success': task.status === 'finished',
              'text-warning': task.status === 'in-progress',
            }"
          >
            {{ capitalizeFirstChar(task.status) }}
          </span>
        </td>
        <td class="text-center">
          <div @click="$emit('deleteTask', index)">
            <span class="fa fa-trash pointer"></span>
          </div>
        </td>
        <td class="text-center">
          <div @click="$emit('editTask', index)">
            <p class="fa fa-pen pointer"></p>
          </div>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "MyTable",
  props: ["tasks"],

  methods: {
    /**
     * Capitalize first character
     */
    capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
  },
};
</script>