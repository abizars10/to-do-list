<template>
  <div>
    <div class="list-task">
      <div 
        v-for="item of tasks" 
        class="item-task d-flek align-items-start border-bottom pt-3 pb-4" 
        :key="item.id"
        :class="{'line-through': item.isDone}"
      >
        <input 
          type="checkbox"
          name="status"
          id="task"
          class="me-2 mt-2"
          :checked="item.isDone"
          @change="markTaskCompleted(item)"
        >
        <div class="d-flex flex-column">
          <div class="title-task mb-1" :class="{'line-through': item.isDone}">
            {{ item.title }}
          </div>
          <div class="description-task small text-muted">
            {{ item.description }}
          </div>
        </div>
        <button class="btn btn-danger btn-sm ms-auto" @click="deleteTask(item.id)">Delete</button>
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
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

export default {
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: 'Task 1',
          description: 'Ini Deskripsi',
          isDone: false,
        }
      ],
      isCreating: false,
      titleValue: '',
      descriptionValue: '',
    }
  },
  methods: {
    addTask() {
      if (this.titleValue && this.descriptionValue) {
        this.tasks.push({
          id: this.tasks.length + 1,
          title: this.titleValue,
          description: this.descriptionValue,
          isDone: false,
        });
        this.titleValue = '';
        this.descriptionValue = '';
        this.isCreating = false;
      }
    },
    deleteTask(taskId) {
      const index = this.tasks.findIndex(task => task.id === taskId);
      if (index !== -1) {
        this.tasks.splice(index, 1);
      }
    },
    markTaskCompleted(item) {
      item.isDone = !item.isDone;
    },
    cancelTask() {
      this.titleValue = '';
      this.descriptionValue = '';
      this.isCreating = false;
    },
    toggleCreatingStatus() {
      this.isCreating = !this.isCreating;
    },
  },
}
</script>

<style scoped>
.line-through {
  text-decoration: line-through;
}
</style>
