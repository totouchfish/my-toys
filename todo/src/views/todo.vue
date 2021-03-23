<template>
  <section>
    <ul class="todo">
      <!-- <Item /> -->
      <Item
        v-for="todo in todoLists"
        :key="todo.id"
        :todo="todo"
        :change="change"
        :deleteTodo="deleteTodo"
      />
    </ul>
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { Todo } from "../types/todo";
import Item from "./item.vue";
export default defineComponent({
  name: "Todo",
  props: {
    todoLists: {
      type: Array as () => Todo[],
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
  components: {
    Item
  }
});
</script>

<style scoped lang="less">
.todo {
  margin-top: 15px;
  text-align: left;
  border: 1px solid #ccc;
  border-radius: 5px;
}
</style>
