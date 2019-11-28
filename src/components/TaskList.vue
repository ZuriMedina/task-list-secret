<template>
  <div>
    <b-container fluid>
      <b-row class="pb-5">
        <b-col>
          <h1 class="pb-5" data-aos="fade-up" data-aos-delay="50">Task List App</h1>
          <b-form-input
            data-aos="fade-down"
            data-aos-delay="100"
            type="text"
            placeholder="New Task"
            v-model="newTask"
            @keyup.enter="addTask"
          ></b-form-input>
        </b-col>
      </b-row>
      <b-row>
        <b-col cols="6" data-aos="fade-right" data-aos-delay="100">
          <b-card class="card">
            <h2 class="pb-5 text-center">To Do</h2>
            <div v-for="task in tasks.slice().reverse()" :key="task.id">
              <b-list-group
                v-if="!task.completed"
                class="pb-2"
                data-aos="fade-in"
                data-aos-delay="100"
              >
                <b-list-group-item>
                  <b-row>
                    <b-col cols="9">
                      <div
                        v-if="!task.editing"
                        @dblclick="editTask(task)"
                        :class="{ completed : task.completed }"
                      >{{ task.title }}</div>
                      <b-form-input
                        v-else
                        class="task-item-edit"
                        type="text"
                        v-model="task.title"
                        @blur="doneEdit(task)"
                        @keyup.enter="doneEdit(task)"
                        @keyup.esc="cancelEdit(task)"
                        v-focus
                      ></b-form-input>
                    </b-col>
                    <b-col>
                      <a variant="outline-primary" @click="completedTask(task)">
                        <i class="fas fa-check pl-5 check"></i>
                      </a>
                    </b-col>
                  </b-row>
                </b-list-group-item>
              </b-list-group>
            </div>
          </b-card>
        </b-col>
        <!-----------------------------------Completedtasks------------------------------->
        <b-col cols="6" data-aos="fade-left" data-aos-delay="100">
          <b-card class="card">
            <h2 class="pb-5 text-center">Done</h2>
            <div v-for="(task, index) in tasks" :key="task.id">
              <b-list-group
                v-if="task.completed"
                class="pb-2"
                data-aos="fade-in"
                data-aos-delay="100"
              >
                <b-list-group-item>
                  <b-row>
                    <b-col cols="9">
                      <div>{{ task.title }} | {{ date }}</div>
                    </b-col>
                    <b-col>
                      <a variant="outline-primary" @click="removeTask(index)">
                        <i class="fas fa-trash pl-5 trash"></i>
                      </a>
                    </b-col>
                  </b-row>
                </b-list-group-item>
              </b-list-group>
            </div>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: 'TaskList',
  data() {
    return {
      newTask: '',
      idForTask: 3,
      beforeEditCache: '',
      date: new Date().toISOString().slice(0, 10),
      tasks: [
        {
          id: 1,
          title: 'Finish Quiz App',
          completed: false,
          editing: false
        },
        {
          id: 2,
          title: 'Finish Task List App',
          completed: false,
          editing: false
        }
      ]
    };
  },
  directives: {
    focus: {
      inserted: function(el) {
        el.focus()
      }
    }
  },
  methods: {
    completedTask(task) {
      task.completed = true
    },
    addTask() {
      if (this.newTask.trim().length == 0) {
        return
      }
      this.tasks.push({
        id: this.idForTask,
        title: this.newTask,
        completed: false,
        editing: false
      });
      this.newTask = ""
      this.idForTask++
    },
    editTask(task) {
      this.beforeEditCache = task.title
      task.editing = true
    },
    doneEdit(task) {
      if (task.title.trim() == '') {
        task.title = this.beforeEditCache
      }
      task.editing = false
    },
    cancelEdit(task) {
      task.title = this.beforeEditCache
      task.editing = false
    },
    removeTask(index) {
      return this.tasks.splice(index, 1)
    }
  }
}
</script>

<style>
.container {
  margin: 100px;
  padding: 50px;
  align-items: center;
  justify-content: center;
  border-radius: 5px;
  background: #fff;
  -webkit-box-shadow: 6px 11px 17px -5px rgba(0, 0, 0, 0.6);
  -moz-box-shadow: 6px 11px 17px -5px rgba(0, 0, 0, 0.6);
  box-shadow: 6px 11px 17px -5px rgba(0, 0, 0, 0.6);
}

.card-body {
  background: #4747d3;
  -webkit-box-shadow: 6px 11px 17px -5px rgba(0, 0, 0, 0.6);
  -moz-box-shadow: 6px 11px 17px -5px rgba(0, 0, 0, 0.6);
  box-shadow: 6px 11px 17px -5px rgba(0, 0, 0, 0.6);
}
.trash {
  cursor: pointer;
  color: #ff0404;
}
.check {
  cursor: pointer;
  color: #04ff04;
}
</style>