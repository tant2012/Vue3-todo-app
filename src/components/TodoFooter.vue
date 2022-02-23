<template>
  <div class="todo-footer" v-show="total">
    <label>
      <!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
      <input type="checkbox" v-model="isAll" />
    </label>
    <span>
      <span>Completed {{ totalDone }}</span> / All {{ total }}</span
    >
    <button class="btn btn-danger" @click="clearAll">Clear selected</button>
  </div>
</template>

<script>
import { computed } from "vue";
export default {
  name: "TodoFooter",
  props: {
    todos: {
      type: Array,
    },
    checkAllTodo: {
      type: Function,
    },
    clearAllTodo:{
      type: Function
    }
  },
  setup(props) {
    const totalDone = computed(() => {
      return props.todos.reduce(
        (pre, current) => pre + (current.done ? 1 : 0),
        0
      );
    });

    const total = computed(() => {
      return props.todos.length;
    });

    const isAll = computed({
      get() {
        return totalDone.value === total.value && total.value > 0;
      },
      set(value) {
        props.checkAllTodo(value);
      },
    });
    // function checkAll(e){
    //   props.checkAllTodo(e.target.checked)
    // }

    function clearAll(){
      props.clearAllTodo()
    }

    return {
      totalDone,
      total,
      isAll,
      // checkAll
      clearAll
    };
  },
};
</script>

<style scoped>
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
