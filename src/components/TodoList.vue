<template>
  <div class="todo-app">
    <h2 style="text-align: initial;">Todo Form</h2>
    <TodoForm @addTodo="addTodo" />
    <div v-if="todos.length > 0">
      <h2>Todo List</h2>
      <div class="table_view">
          <table>
            <thead>
              <tr>
                <th>Title</th>
                <th>Priority</th>
                <th>Due Date</th>
                <th>Description</th>
                <th>Status</th>
                <th>Actions</th>
              </tr>
            </thead>
            <tbody>
              <TodoItem v-for="(todo,index) in todos" :key="index" :todo="todo" @deleteTodo="deleteTodo(index)" @toggleComplete="completeTodo(index)" />
            </tbody>
          </table>
        </div>
      </div>
  </div>
</template>

<script>
import TodoItem from './TodoItems.vue'
import TodoForm from './TodoForm.vue'

export default {
  components: {
    TodoItem,
    TodoForm
  },
  data() {
    return {
      todos: []
    }
  },
  created() {
    this.loadTodosFromLocalStorage();
  },
  methods: {
    addTodo(todo) {
      this.todos.push(todo);
      this.saveTodosToLocalStorage();
    },
    deleteTodo(index) {
      console.log("index",index)
      this.todos.splice(index,1)
      console.log("dhfjh",this.todos)
      this.saveTodosToLocalStorage();
    },
    completeTodo(index) {
        this.todos[index].completed = !this.todos[index].completed;
        this.saveTodosToLocalStorage();
    },
    loadTodosFromLocalStorage() {
      const todos = localStorage.getItem('todos');
      if (todos) {
        this.todos = JSON.parse(todos);
      }
    },
    saveTodosToLocalStorage() {
      localStorage.setItem('todos', JSON.stringify(this.todos));
    }
  }
}
</script>
<style scoped>
  table {
    width: 100%;
    border-collapse: collapse;
  }

  th, td {
    padding: 8px;
    border: 1px solid #ddd;
  }

  th {
    background-color: #f2f2f2;
  }

  button {
    margin-right: 5px;
  }
  .table_view {
    margin-top:30px;
    overflow-x: auto;
  }
</style>