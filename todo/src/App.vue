<template>
  <div class="main">
    <Header :addTodo="addTodo" />
    <List
      :change="changeStatus"
      :todoLists="todoLists"
      :deleteTodo="deleteTodo"
    />
    <Footer :todoLists="todoLists" :operateAll="operateAll" :clear="clear" />
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, toRefs } from "vue";
import Header from "./views/header.vue";
import List from "./views/todo.vue";
import Footer from "./views/footer.vue";
import { Todo } from "./types/todo";
export default defineComponent({
  name: "App",
  components: {
    Header,
    List,
    Footer
  },
  setup() {
    // 用泛型来约束todoLists reactive<ITodo []>
    // state是一个对象，所以用对象的方式来约束 reactive<{todoLists: ITodo []}>
    const state = reactive<{ todoLists: Todo[] }>({
      todoLists: [
        {
          id: 1,
          title: "吃饭",
          isCompleted: true
        },
        {
          id: 2,
          title: "睡觉",
          isCompleted: false
        },
        {
          id: 3,
          title: "打豆豆",
          isCompleted: false
        }
      ]
    });
    // 修改
    const changeStatus = (val: boolean, todo: Todo) => {
      todo.isCompleted = val;
    };
    // 新增
    const addTodo = (todo: Todo) => {
      state.todoLists.unshift(todo);
    };
    // 删除
    const deleteTodo = id => {
      const index = state.todoLists.findIndex(todo => todo.id === id);
      state.todoLists.splice(index, 1);
    };
    // 清除已完成todo
    const clear = () => {
      state.todoLists = state.todoLists.filter(
        todo => todo.isCompleted === false
      );
    };
    // 处理全部数据
    const operateAll = (val: boolean) => {
      state.todoLists.forEach(todo => {
        todo.isCompleted = val;
      });
    };
    return {
      ...toRefs(state),
      changeStatus,
      addTodo,
      deleteTodo,
      clear,
      operateAll
    };
  }
});
</script>
<style lang="less">
.main {
  width: 50%;
  margin: auto;
  text-align: center;
  border: 1px solid #ccc;
  padding: 15px;
  margin-top: 30px;
  border-radius: 5px;
}
</style>
