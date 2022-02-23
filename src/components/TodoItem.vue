<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="todo.done"
        @change="handleCheck(todo.id)"
      />
      <span v-show="!todo.isEdit">{{ todo.title }} </span>
      <input
        v-show="todo.isEdit"
        type="text"
        :value="todo.title"
        @blur="handleBlur(todo, $event)"
      />
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">
      Remove
    </button>
    <button class="btn btn-edit" @click="handleEdit(todo)">Edit</button>
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
      type: Function,
    },
    deleteTodo: {
      type: Function,
      required: true,
    },
  },

  setup(props) {
    //  tick or untick checkbox
    function handleCheck(id) {
      // reverse the value of done in todo obj through App.vue
      props.checkTodo(id);
    }

    // remove todo obj through app.vue
    function handleDelete(id) {
      // delete
      if (confirm("Are you sure you want to delete?")) props.deleteTodo(id);
    }

    // declare isEdit value
    function handleEdit(todo) {
      todo.isEdit = true;
    }

    // save edited title through user input
    function handleBlur(todo, e) {
      todo.isEdit = false;
      todo.title = e.target.value;
    }
    return { handleCheck, handleDelete, handleEdit, handleBlur };
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
