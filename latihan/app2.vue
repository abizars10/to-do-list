<template>
  <div class="list-task">
    <div v-for="item of tasks" class="item-task d-flek align-items-start border-bottom pt-3 pb-4" :key="item.id">
      <input 
      type="checkbox"
      name="status"
      id="task"
      class="me-2 mt-2"
      :checked="item.isDone"
      >
      <div class="d-flex flex-column">
        <div class="title-task mb-1">
          {{ item.title }}
        </div>
        <div class="description-task small text-muted">
          {{ item.description }}
        </div>
      </div>
    </div> 
    
    <div class="action py-2">
      <!-- Jika isCreating == false maka tombol Add Task tidak akan tampil -->
      <!-- isCreating = !isCreating berfungsi sebagai switcher toggle -->
      <a href="#" class="add-button" v-if="!isCreating" @click="isCreating = !isCreating">Add Task</a>
      <div class="add-card" v-else>
        <div class="card mb-2">
          <div class="card-body d-flex flex-column p-0">
            <input v-model="titleValue" class="form-control border-0 mb-2" placeholder="Title" type="text">
            <textarea v-model="descriptionValue" class="form-control border-0 small" placeholder="Description" rows="3"></textarea>
          </div>
        </div>
        <div class="button-wrapper d-flex">
          <button class="btn btn-primary me-2" @click="addTask">save</button>
          <button class="btn btn-outline-secondary" @click="isCreating = !isCreating">cancel</button>
        </div>
      </div>
    </div>
</div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

export default{
  data() {
    return {
      //Daftar Task
      tasks: [
        {
          id: 1,
          title: 'Task 1',
          description: 'Ini Deskripsi',
          isDone: false,
        }
      ],
      // Status saat menambahkan tasks
      isCreating: false,
      titleValue: '',
      descriptionValue: '',
    }
  },
  methods: {
    addTask() {
      console.log('title: ', this.titleValue);
      console.log('description: ', this.descriptionValue);
      this.tasks.push({
        id: this.tasks.length + 1,
        title: this.titleValue,
        description: this.descriptionValue,
        isDone: false,
      })
      console.log(this.tasks);
    },
  }
}
</script>
