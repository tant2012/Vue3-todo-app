<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <todo-header :addTodo="addTodo"></todo-header>
        <todo-list
          :todos="todos"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
        ></todo-list>
        <todo-footer
          :todos="todos"
          :checkAllTodo="checkAllTodo"
          :clearAllTodo="clearAllTodo"
        ></todo-footer>
      </div>
    </div>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader";
import TodoList from "./components/TodoList";
import TodoFooter from "./components/TodoFooter";
import { ref, watch } from "vue";

export default {
  name: "App",
  components: {
    TodoHeader,
    TodoList,
    TodoFooter,
  },
  setup() {

    // declare todos
    let todos = ref(JSON.parse(localStorage.getItem("todos")) || []);

    // add
    function addTodo(todoObj) {
      todos.value.unshift(todoObj);
    }

    //delete
    function deleteTodo(id) {
      todos.value = todos.value.filter((todo) => todo.id !== id);
    }

    function clearAllTodo() {
      todos.value = todos.value.filter((todo) => {
        return !todo.done;
      });
    }

    //check
    function checkTodo(id) {
      todos.value.forEach((todo) => {
        if (todo.id === id) todo.done = !todo.done;
      });
    }

    function checkAllTodo(done) {
      todos.value.forEach((todo) => {
        todo.done = done;
      });
    }

    //save data in local storage
    watch(
      () => todos.value,
      function handler(value) {
        localStorage.setItem("todos", JSON.stringify(value));
      },
      { deep: true }
    );

    return {
      todos,
      addTodo,
      checkTodo,
      deleteTodo,
      checkAllTodo,
      clearAllTodo,
    };
  },
};
</script>

<style>
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-edit {
  color: #fff;
  background-color: rgb(2, 181, 252);
  border: 1px solid rgb(0, 187, 255);
  margin-right: 5px;
}

.btn-edit:hover {
  color: #fff;
  background-color: skyblue;
  margin-right: 5px;
}
.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
