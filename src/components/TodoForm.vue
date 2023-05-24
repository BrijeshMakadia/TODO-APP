<template>
  <form @submit.prevent="submitForm" class="todo-form">
    <div class="form-field">
        <label for="title">Title:</label>
        <input type="text" id="title" v-model.trim="title" @input="validateFormTitle" placeholder="Enter Title" />
        <p v-if="errors.title" class="error-message">{{ errors.title }}</p>
    </div>
    <div class="form-field">
        <label for="priority">Priority:</label>
        <select id="priority" v-model="priority">
            <option value="low">Low</option>
            <option value="medium">Medium</option>
            <option value="high">High</option>
        </select>
        <p v-if="errors.priority" class="error-message">{{ errors.priority }}</p>
    </div>
    <div class="form-field">
        <label for="due-date">Due Date:</label>
        <input type="date" id="due-date" v-model="dueDate" @input="validateFormDueDate()" />
        <p v-if="errors.dueDate" class="error-message">{{ errors.dueDate }}</p>
    </div>
     <div class="form-field">
        <label for="description">Description:</label>
        <textarea id="description" v-model.trim="description" @input="validateFormDes" placeholder="Enter Description"></textarea>
        <p v-if="errors.description" class="error-message">{{ errors.description }}</p>
    </div>
    <button type="submit" class="button">Add Todo</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
        title: '',
        description: '',
        priority: 'low',
        dueDate: '',
        errors: {}
    }
  },
  methods: {
    submitForm() {
        this.validateForm()
        if(this.errors.dueDate !== '' || this.errors.description !== '' || this.errors.title !== ''){
            return;
        }
        const todo = {
            title: this.title,
            description: this.description,
            priority: this.priority,
            dueDate: this.dueDate,
            completed: false
        }
        this.$emit('addTodo', todo)
        this.resetForm()
      
    },
    validateForm() {
        this.errors = {}
        this.validateFormTitle();
        this.validateFormDes();
        this.validateFormDueDate();
        return Object.keys(this.errors).length === 0;
    },
    validateFormTitle() {
        if (!this.title) {
            this.errors.title = 'Title field is required.'
        }else {
            this.errors.title = ''
        }
    },
    validateFormDes(){
        if (!this.description) {
            this.errors.description = 'Description field is required'
        }else {
            this.errors.description = ''
        }
    },
    validateFormDueDate(){
        if (!this.dueDate) {
            this.errors.dueDate = 'DueDate field is required'
        }else {
            this.errors.dueDate = ''
        }
    },
    resetForm() {
        this.title = ''
        this.description = ''
        this.priority = 'low'
        this.dueDate = ''
    }
  }
}
</script>

<style scoped>
.form-field {
    margin-bottom: 30px;
    position: relative;
}

.error-message {
    color: red;
    margin: 0px;
    position: absolute;
    bottom: -10px;
    font-size:14px;
}
.todo-form input[type="text"],
.todo-form textarea,
.todo-form select,
.todo-form input[type="date"] {
  width: 100%;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 3px;
  margin-bottom: 10px;
}
.todo-form textarea {
    resize:none;
}
.todo-form {
    width: 100%;
    max-width: 280px;
    text-align: initial;
}
.button {
    background-color: #4CAF50; /* Green */
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    cursor: pointer;
    border-radius:5px;
}
</style>