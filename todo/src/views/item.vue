<template>
  <li
    class="todo-item"
    @mouseover="handleMouse(true)"
    @mouseout="handleMouse(false)"
  >
    <label>
      <input type="checkbox" v-model="isCompleted" /><span>{{
        todo.title
      }}</span>
      <button
        class="todo-button"
        v-show="isShowDelete"
        @click="deleteTodo(todo.id)"
      >
        删除
      </button>
    </label>
  </li>
</template>

<script lang="ts">
import { defineComponent, computed, ref } from "vue";
import { Todo } from "../types/todo";
export default defineComponent({
  name: "Item",
  props: {
    todo: {
      type: Object as () => Todo,
      require: true
    },
    change: {
      type: Function,
      require: true
    },
    deleteTodo: {
      type: Function,
      require: true
    }
  },
  setup(props) {
    const isCompleted = computed({
      get() {
        return props.todo.isCompleted;
      },
      set(val) {
        return props.change(val, props.todo);
      }
    });
    const isShowDelete = ref(false);
    function handleMouse(flag) {
      isShowDelete.value = flag;
    }
    return {
      isCompleted,
      handleMouse,
      isShowDelete
    };
  }
});
</script>

<style scoped lang="less">
.todo-item {
  padding: 5px;
  height: 30px;
  line-height: 30px;
  border-bottom: 1px solid #ccc;
  &:last-child {
    border-bottom: 0;
  }
  span {
    padding-left: 5px;
  }
  button {
    float: right;
    margin-top: 3px;
  }
}
</style>
