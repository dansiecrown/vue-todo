<template>
  <div class="title">TODOS</div>
  <div v-show="!filteredTodos.length" class="empty">Your todo list is currently empty, add some below!</div>
  <ul>
    <li v-for="(todo, i) in filteredTodos" :key="i" class="todo-item">
      <span :class="todo.isCompleted? 'has-line-through': ''">👉 {{ todo.name }}</span>
      <button class="delete-btn" @click="removeTodo(todo, i)">Delete</button>
      <button  @click="todo.isCompleted? updateTodo(todo):markComplete(todo)">{{todo.isCompleted? "Not Complete":"Complete"}}</button>
      
    </li>
  </ul>

  <div class="input-container">
    <input type="text" v-model="todo" />

    <button class="add-btn" @click="addTodo" :disabled="!todo">Add Todo</button>
  </div>


<p><i>Write your todo task and click the "Add Todo" button.</i></p>


</template>

<script>
export default {
  name: "App",
  data() {
    return {
      todo: "",
      todos: [
        
      ],
      removed: [

      ],
    }
    
    ;
  },
  computed: {
    filteredTodos() {
      return this.todos.filter((todo) => !todo.deleted);
    },
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length + 1,
        name: this.todo,
        isCompleted: false,
        deleted: false,

      })
      
      this.todo = "";
    },
    removeTodo(x) {
      x.deleted = true
    },
    updateTodo(x) {
      x.isCompleted = false
    },
    markComplete(x) {
      x.isCompleted = true
    },
  },
};
</script>

<style>
.title {
  margin-bottom: 15px;
  font-size: 18px;
  font-weight: 600;
}

.add-btn {
  margin-left: 5px;
}

.delete-btn {
  margin-right: 5px;
  margin-left: 20px;
}

.input-container {
  margin-top: 20px;
}

.todo-item {
  margin-bottom: 10px;
}

.has-line-through {
  text-decoration: line-through;
}
</style>
