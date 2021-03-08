<template>
  <div class="container">
  <h1>TODO APP</h1>
    <div class="addTask">
  <input
      class="input_task"
      type="text"
      v-model="taskInput"
      placeholder="Добавьте задачу"
      @keyup.enter="addTask"
  >
  <button @click="addTask">Добавить</button>
    </div>

    <div class="tasks_list">
  <ul>
    <li
        v-for="(task, idx) in tasks"
        :key="task.id"
        :class="task.checked ? 'done' : ''"
        class="task"
    >
      <span>

      <span :class="task.checked ? 'dNone' : ''">
        <input class="checkbox" @click="check(task.id)" type="checkbox">
      </span>

        <input
            v-if="task.edit"
            v-model="form.text"
            @keyup.enter="changeTask"
            type="text" />

      <span v-else @dblclick="showForm(idx)">{{ task.title }}</span>

      </span>
      <button @click="removeTask(task.id)" class="delete">X</button>
    </li>
  </ul>
    </div>
    <p v-if="tasks.length === 0">Список задач пуст.</p>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      taskInput: '',
      clickedIndex: Number,
      form: {
        text: ''
      },
      tasks: [
        {
          title: 'Первая задача',
          checked: false,
          edit: false,
          id: 567
        },
        {
          title: 'Вторая задача',
          checked: false,
          edit: false,
          id: 568
        },
        {
          title: 'Третья задача',
          checked: false,
          edit: false,
          id: 569
        },
      ],

    }
  },
  methods: {
    check(index) {
      for (let i of this.tasks) {
        if (i.id === index) {
          i.checked = true
        }
      }
    },
    addTask() {
      let newTask = {
        title: this.taskInput,
        checked: false,
        edit: false,
        id: Math.random()
      }
      this.tasks.push(newTask)
      this.taskInput = ''
    },
    removeTask(id) {
      this.tasks = this.tasks.filter(t => t.id !== id)
    },
    showForm(id) {
      this.tasks[id].edit = true
      this.clickedIndex = id
      this.form.text = this.tasks[id].title
    },
    changeTask() {
      this.tasks[this.clickedIndex].title = this.form.text
      this.tasks[this.clickedIndex].edit = false
    }
  },
}
</script>

<style>
body {
  font-family: Inter, Roboto, Oxygen, Fira Sans, Helvetica Neue, sans-serif;
  background: #6593aa;
  color: #fff;
}

.task {
  display: flex;
  justify-content: space-between;
  list-style-type: none;
  cursor: pointer;
  border: 1px solid #00ffb1;
  border-radius: 10px;
  background: #fff;
  color: black;
  padding: 10px;
  margin-bottom: 5px;
}

.input_task {
  width: 300px;
  font-size: 13px;
  padding: 6px 0 4px 10px;
  border: 1px solid #cecece;
  background: #F6F6f6;
  border-radius: 8px;
}

  button {
    border: 1px solid limegreen;
    border-radius: 40px;
    width: 150px;
    height: 30px;
    margin-left: 10px;
  }
  button:active {
    border: 3px solid lightseagreen;
  }

  button:active, button:focus, input:active, input:focus {
    outline: none;
  }
  button::-moz-focus-inner {
    border: 0;
  }
  .delete {
    border: 1px solid red;
    width: 25px;
    height: 25px;
    background: #ed9d9d;
  }
.delete:active {
  border: 3px solid crimson;
}
  .done {
    color: #7d7e82;
    text-decoration: line-through;
  }
  .dNone {
    display: none;
  }
  .container {
    margin: 0 auto;
    max-width: 650px;
    display: flex;
    flex-direction: column;
  }

  .container h1{
    margin: 15px auto;
  }

  .addTask {
    display: flex;
    margin: 0 auto;
    width: 100%;
    border-radius: 3px;
  }
  .tasks_list ul{
    padding-left: 0;
  }
  .checkbox {
    margin-right: 10px;
  }
</style>