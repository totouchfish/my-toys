<template>
  <section class="footer">
    <label>
      <input type="checkbox" v-model="isAllcompleted" />
      已完成{{ isCompleted }}/全部{{ todoLists.length }}
    </label>
    <button class="todo-button" @click="clear">清除已完成任务</button>
  </section>
</template>

<script lang="ts">
import { defineComponent, computed } from "vue";
import { Todo } from "@/types/todo";
export default defineComponent({
  name: "Footer",
  props: {
    todoLists: {
      type: Array as () => Todo[],
      require: true
    },
    clear: {
      type: Function,
      require: true
    },
    operateAll: {
      type: Function,
      require: true
    }
  },
  setup(props) {
    const isCompleted = computed(() => {
      return props.todoLists.reduce((acc, cur) => {
        return acc + (cur.isCompleted ? 1 : 0);
      }, 0);
    });
    const isAllcompleted = computed({
      get() {
        return props.todoLists.every(todo => todo.isCompleted);
      },
      set(val) {
        props.operateAll(val);
      }
    });
    return {
      isCompleted,
      isAllcompleted
    };
  }
});
</script>

<style scoped lang="less">
.footer {
  margin: 20px 0 5px 5px;
  text-align: left;
  button {
    float: right;
  }
}
</style>
