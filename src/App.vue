<template>
  <div class="container">
    <Header title="Task Tracker" />
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'

@Options({
  components: {
    Header,
    Tasks
  },
  data() {
    return {
      tasks: []
    }
  },
  methods: {
    deleteTask(id: number) {
      if (confirm('Are you sure ?')) {
        this.tasks = this.tasks.filter(
          (task: {
            id: number
            text: string
            day: string
            reminder: boolean
          }) => task.id !== id
        )
      }
    },

    toggleReminder(id: number) {
      this.tasks = this.tasks.map(
        (task: { id: number; text: string; day: string; reminder: boolean }) =>
          task.id === id ? { ...task, reminder: !task.reminder } : task
      )
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'D Appointment',
        day: 'March 1st at 2:30pm',
        reminder: true
      },
      {
        id: 2,
        text: 'D Appointment2',
        day: 'March 2nd at 2:00pm',
        reminder: true
      },
      {
        id: 3,
        text: 'D Appointment3',
        day: 'March 2nd at 2:20pm',
        reminder: false
      }
    ]
  }
})
export default class App extends Vue {}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&dis1play=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
