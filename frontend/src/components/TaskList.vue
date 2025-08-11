<template>
  <div>
    <h2>Tasks</h2>
    <div v-if="loading">Loading...</div>
    <div v-else>
      <div v-if="tasks.length===0">No tasks yet. Add one above.</div>
      <div v-for="task in tasks" :key="task._id" style="border:1px solid #ddd;padding:12px;margin:8px 0;border-radius:6px;">
        <div style="display:flex;justify-content:space-between;align-items:center;">
          <div>
            <strong>{{ task.title }}</strong>
            <div style="font-size:13px;color:#555">{{ task.description }}</div>
            <div style="font-size:12px;color:#888">Status: {{ task.status }}</div>
          </div>
          <div>
            <button @click="$emit('edit-task', task)" style="margin-right:8px;">Edit</button>
            <button @click="removeTask(task._id)">Delete</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { getTasks, deleteTask } from '../services/taskService';
export default {
  data(){ return { tasks: [], loading: true }; },
  async mounted(){ await this.loadTasks(); },
  methods:{
    async loadTasks(){
      this.loading = true;
      try{
        const res = await getTasks();
        this.tasks = res.data;
      }catch(e){
        console.error(e);
        alert('Could not load tasks. Make sure backend is running.');
      }finally{ this.loading = false; }
    },
    async removeTask(id){
      if(!confirm('Delete this task?')) return;
      try{
        await deleteTask(id);
        this.tasks = this.tasks.filter(t=>t._id !== id);
      }catch(e){ console.error(e); alert('Delete failed'); }
    }
  }
}
</script>
