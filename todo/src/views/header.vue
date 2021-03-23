<template>
  <section class="header">
    <input type="text" v-model="title" @keyup.enter="add" />
  </section>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import { Todo } from "@/types/todo";
export default defineComponent({
  name: "Header",
  props: {
    todoLists: {
      type: Array as () => Todo[],
      require: true
    },
    addTodo: {
      type: Function,
      require: true
    }
  },
  setup(props) {
    const title = ref("");
    const add = () => {
      if (!title.value) return;
      let id = 1;
      if (props.todoLists && props.todoLists.length) {
        id = props.todoLists[props.todoLists.length].id + 1;
      }
      const obj: Todo = {
        id,
        title: title.value,
        isCompleted: false
      };
      title.value = "";
      return props.addTodo(obj);
    };
    return {
      title,
      add
    };
  }
});
</script>

<style scoped lang="less">
.header {
  input {
    width: 100%;
    font-size: 20px;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-sizing: border-box;
    &:focus {
      outline: 0;
      border: 1px solid transparent;
      box-shadow: 0px 0px 8px 0px #1a71cc;
    }
  }
}
</style>
