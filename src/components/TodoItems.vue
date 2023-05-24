<template>
    <tr class="table_body">
        <th>{{ todo.title }}</th>
        <th>{{ todo.priority }}</th>
        <th>{{ todo.dueDate }}</th>
        <th>{{ todo.description }}</th>
        <th>{{ todo.completed ? 'Completed' : 'Pending' }}</th>
        <th>
            <button class="delete" @click="deleteTodo()">Delete</button>
            <button @click="toggleComplete" class="mark">
                {{ todo.completed ? 'Mark Incomplete' : 'Mark Complete' }}
            </button>
        </th>
    </tr>
  
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  methods: {
    deleteTodo() {
      this.$emit('deleteTodo', this.todo)
    },
    toggleComplete() {
      this.$emit('toggleComplete', this.todo)
    }
  }
}
</script>
<style scoped>
table {
    width: 100%;
    border-collapse: collapse;
}
.table_body th {
    border: 1px solid #ddd;
    padding: 10px;
}

button {
    margin-right: 5px;
}
.delete {
    background-color: red;
    border: none;
    color: white;
    padding: 5px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    border-radius:5px;
    cursor: pointer;
}
.mark {
    background-color: Green;
    border-radius:5px;
    border: none;
    color: white;
    padding: 5px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    cursor: pointer;
}
</style>