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
        <todo-footer></todo-footer>
      </div>
    </div>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader";
import TodoList from "./components/TodoList";
import TodoFooter from "./components/TodoFooter";
import {  reactive } from "vue";

export default {
  name: "App",
  components: {
    TodoHeader,
    TodoList,
    TodoFooter,
  },
  setup() {
    let todos = reactive([
      { id: "001", title: "a", done: true },
      { id: "002", title: "b", done: false },
      { id: "003", title: "c", done: true },
    ]);

    function addTodo(todoObj) {
      todos.unshift(todoObj);
    }

    function checkTodo(id) {
      todos.forEach((todo) => {
        if (todo.id === id) todo.done = !todo.done;
      });
    }

    function deleteTodo(id) {
      console.log(todos)
		todos = todos.filter( todo => todo.id !== id )
      console.log(todos)
      
    }
    return {
      todos,
      addTodo,
      checkTodo,
      deleteTodo,
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
