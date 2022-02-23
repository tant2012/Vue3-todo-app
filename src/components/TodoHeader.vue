<template>
  <div class="todo-header">
    <input
      type="text"
      placeholder="Please enter your task"
      v-model="title"
      @keyup.enter="add"
    />
  </div>
</template>

<script>
import { nanoid } from "nanoid";
import { ref } from "vue";
export default {
  name: "TodoHeader",
  props: {
    addTodo: {
      type: Function,
      required: true
    },
  },
  setup(props) {
    let title = ref("");
    function add() {
      const text = title.value;
      if (!text.trim()) return alert("Please enter something");
      const todoObj = {
        id: nanoid(),
        title: text,
        done: false,
      };
      props.addTodo(todoObj);
      title.value = "";
    }
    return {
      title,
      add,
    };
  },
};
</script>

<style scoped>
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
