<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="todo.done"
        @change="handleCheck(todo.id)"
      />
      <span>{{ todo.title }}</span>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">delete</button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    todo: {
      type: Object,
      required: true,
    },
    checkTodo: {
      type: Function
      
    },
    deleteTodo: {
      type: Function,
      required: true,
    },
  },
  setup(props) {
    function handleCheck(id) {
      props.checkTodo(id);
    }

    function handleDelete(id) {
      if (confirm("Are you sure you want to delete?")) 
      props.deleteTodo(id);
    }

    return { handleCheck, handleDelete };
  },
};
</script>

<style scoped>
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover {
  background-color: lightgray;
}
li:hover button {
  display: block;
}
</style>
