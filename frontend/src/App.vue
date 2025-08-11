<template>
  <div style="max-width:800px;margin:40px auto;font-family:Arial,Helvetica,sans-serif">
    <h1>Task Manager</h1>
    <AddTask @task-added="refresh" :editingTask="editingTask" @cancel-edit="cancelEdit" />
    <TaskList @edit-task="startEdit" />
  </div>
</template>

<script>
import TaskList from './components/TaskList.vue';
import AddTask from './components/AddTask.vue';

export default {
  components: { TaskList, AddTask },
  data(){ return { editingTask: null }; },
  methods:{
    startEdit(task){ this.editingTask = task; window.scrollTo({top:0,behavior:'smooth'}); },
    cancelEdit(){ this.editingTask = null; },
    refresh(){ this.editingTask = null; this.$refs && this.$refs.taskList && this.$refs.taskList.loadTasks && this.$refs.taskList.loadTasks(); }
  }
}
</script>
