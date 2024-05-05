<template>
  <div class="container">
    <h2>Manage Tasks in WAR</h2>

    <table>
      <thead>
        <th>Task category</th>
        <th>Planned task</th>
        <th>Description</th>
        <th>Planned hours</th>
        <th>Actual hours</th>
        <th>Status</th>
        <th></th>
      </thead>

      <tbody>
        <tr v-for="task in this.tasks">
          <td>{{task.category}}</td>
          <td>{{task.plannedTask}}</td>
          <td>{{task.description}}</td>
          <td>{{task.plannedHours}}</td>
          <td>{{task.actualHours}}</td>
          <td>{{task.status}}</td>
          <td>
            <button @click="this.editTask">Edit</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    data() {
      return{
        tasks: [
          {
            category: "enhance",
            plannedTask: "implement Instructor class",
            description: "implement Instructor class",
            plannedHours: 5,
            actualHours: 0,
            status: 'Done'
          },
          {
            category: "enhance",
            plannedTask: "implement Student class",
            description: "implement Student class",
            plannedHours: 5,
            actualHours: 0,
            status: 'In Progress'
          }
        ],
      };
    },

    methods: {
      editTask: function() {
        console.log("The edit button has been clicked.")
      }
    }
  }
</script>