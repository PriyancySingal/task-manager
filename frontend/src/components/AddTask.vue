<template>
  <div style="margin-bottom:20px;padding:12px;border:1px solid #eee;border-radius:8px;">
    <h3>{{ editingTask ? 'Edit Task' : 'Add Task' }}</h3>
    <form @submit.prevent="submit">
      <div style="margin-bottom:8px;">
        <input v-model="form.title" placeholder="Title" required style="width:100%;padding:8px;border-radius:4px;border:1px solid #ccc" />
      </div>
      <div style="margin-bottom:8px;">
        <textarea v-model="form.description" placeholder="Description" rows="3" style="width:100%;padding:8px;border-radius:4px;border:1px solid #ccc"></textarea>
      </div>
      <div style="margin-bottom:8px;">
        <select v-model="form.status" style="padding:6px;">
          <option>Pending</option>
          <option>Completed</option>
        </select>
      </div>
      <div>
        <button type="submit">{{ editingTask ? 'Update' : 'Add' }}</button>
        <button type="button" v-if="editingTask" @click="$emit('cancel-edit')">Cancel</button>
      </div>
    </form>
  </div>
</template>

<script>
import { addTask, updateTask } from '../services/taskService';
export default {
  props:['editingTask'],
  data(){ return { form:{ title:'', description:'', status:'Pending' } }; },
  watch:{ editingTask(newVal){ if(newVal) this.form = { title:newVal.title, description:newVal.description, status:newVal.status }; else this.form = { title:'', description:'', status:'Pending' }; } },
  methods:{
    async submit(){
      try{
        if(this.editingTask){
          await updateTask(this.editingTask._id, this.form);
          alert('Updated');
        } else {
          await addTask(this.form);
          alert('Added');
        }
        this.$emit('task-added');
        this.form = { title:'', description:'', status:'Pending' };
      }catch(e){
        console.error(e);
        alert('Operation failed. Is backend running?');
      }
    }
  }
}
</script>
