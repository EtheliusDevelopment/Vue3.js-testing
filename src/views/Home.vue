<template>

<div>
          <div v-show="showAddTask" >
      <AddTask @add-task="addTask"/>
    </div>
    <Tasks
      @toogle-reminder='toogleReminder'
      @delete-task='deleteTask'
      :tasks='tasks'
    />      
</div>  
    
</template>

<script>
import Tasks from '../components/Tasks.vue';
import AddTask from '../components/AddTask.vue';

export default {

name: 'Home',
props: {
    showAddTask: Boolean,
}, 
components: {
    Tasks,
    AddTask
},
data () {
    return {
        tasks: [],
    }
},

  async created() {
    this.tasks = await this.fetchTasks()
  },

  methods: {
    async deleteTask(id) {
      if (window.confirm('Are you sure?')) {
        const res = await fetch(`api/tasks/${id}`, {
         method: 'DELETE',
        });
        
        res.status == 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert('Error Deleting Task')
       }
    },
    toogleReminder(id) {
      this.tasks = this.tasks.map((task) => 
         task.id === id ? { ...task, reminder: !task.reminder } : task
      );
      
    },
    async addTask(task) {
       const res = fetch('api/tasks/', {
         method: 'POST',
         headers: {
           'Content-type': 'application/json',
           },
         body: JSON.stringify(task)
       });
       const data = await (await res).json();
        this.tasks = [...this.tasks, data]
    },
 
    async fetchTasks() {
      const res = fetch('api/tasks/');
      const data = await (await res).json();
      return data
    },
        async fetchTask(id) {
      const res = fetch(`api/tasks/${id}`);
      const data = await (await res).json();
      return data
    },
  },

}

</script>