<template>
  <div class="todo">
    <div class="card text-left">
      <div class="card-header">
        ToDo Component
      </div>
      <div class="card-body">
        <button @click="isOpen = true">Create a new task</button>
        <Popup :open="isOpen" @close="isOpen = !isOpen">
          <form>
            <div class="form-group">
              <label for="task-title">Task title</label>
              <input v-model="model.title" type="text" class="form-control" id="task-title"
                     aria-describedby="emailHelp">
            </div>
            <div class="form-group">
              <label for="task-type">Type:</label>
              <select v-model="model.type" name="cars" class="form-control" id="task-type">
                <option value="critical">Critical</option>
                <option value="high">High</option>
                <option value="medium">Medium</option>
                <option value="low">Low</option>
              </select>
            </div>
            <div class="form-group">
              <label for="task-desc">Task description</label>
              <textarea v-model="model.description" class="form-control" id="task-desc"></textarea>
            </div>
            <button type="submit" class="btn btn-primary" @click.prevent="submit" :disabled="!isValid">Submit</button>
          </form>
        </Popup>
        <h5 class="card-title">My tasks</h5>
        <div class="card-text">
          
          <ul class="pt-3">
            <li v-for="(item, index) in filteredTaskList" :key="index" class="d-flex justify-content-between mb-3">
              <div>
                <h4 :class="item.type" v-if="item.status === 'completed'"><s>{{item.title}}</s></h4>
                <h4 :class="item.type" v-else>{{item.title}}</h4>
                <p>{{item.description}}</p>
              </div>
              <div v-if="item.status != 'completed'" >
                <button class="btn btn-primary" @click="item.status = 'completed' ">Compled</button>
              </div>
        
            </li>
          </ul>
        </div>
        <div class="card-footer">
          <button class="btn" :class="{'btn-primary':!filterStatus}" @click="filterStatus = ''">All</button>
          <button class="btn" :class="{'btn-primary': filterStatus === 'completed'}"
                  @click="filterStatus = 'completed'">Completed
          </button>
          <button class="btn" :class="{'btn-primary': filterStatus === 'incompleted'}"
                  @click="filterStatus = 'incompleted'">InCompleted
          </button>
          Active tasks count: {{ taskList.length }}
        </div>
      </div>
    </div>
  </div>
</template>


<script>
  import {Task} from '../models/task';
  import Popup from './Popup.vue';
  import { ref } from "@vue/composition-api"
  export default {
    name: "ToDo",
    props: {},
    data: () => {
      return {
        isOpen: false,
        model: new Task(),
        taskList: [],
        filterStatus: "",
      }
    },
    methods: {
      submit() {
        this.taskList.push(this.model);
        console.log(this.taskList);
        this.model = new Task();
      }
    },
    watch: {
      message() {
        console.log("Nessage changed");
      },
      setup() {
      const isOpen = ref(false);

      return { isOpen };
    }
    },
    computed: {
      messageLength() {
        return ("" + this.message).length;
      },
      isValid() {
        return this.model.title && this.model.description && this.model.type;
      },
      
      filteredTaskList() {
        return this.taskList.filter((item) => {
          if (!this.filterStatus) return true;
          return item.status === this.filterStatus;
        });
      }
    },
    components: {
      Popup
    }

  }

  
</script>

<style scoped>
  .todo {
    background-color: aqua;
  }

  .critical {
    background-color: red;
  }
  .high {
    background-color: pink;
  }

  .medium {
    background-color: green;
  }

  .low {
    background-color: blue;}
  
</style>

