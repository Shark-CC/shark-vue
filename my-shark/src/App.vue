<template>
  <div id="app">
    //2月27
    <div class="todo-container">
      <div class="todo-wrap">
        <todo-header></todo-header>
        <todo-list :listArr="listArr"></todo-list>
        <todo-footer></todo-footer>
      </div>
    </div>
  </div>
</template>

<script>
import todoHeader from "./components/todoHeader";
import todoList from "./components/todoList";
import todoFooter from "./components/todoFooter";

export default {
  name: "App",
  data() {
    return {
      listArr: [
        { id: 0, content: "aaaa", checked: false },
        { id: 1, content: "bbbb", checked: false },
        { id: 2, content: "cccc", checked: false }
      ]
    };
  },
  methods: {
    addTodo(item) {
      this.listArr.unshift(item);
    },
    clear() {
      this.listArr = this.listArr.filter(item => {
        return !item.checked;
      });
    }
  },
  components: {
    "todo-header": todoHeader,
    "todo-list": todoList,
    "todo-footer": todoFooter
  },
  mounted() {
    this.bus.$on("delTodo", id => {
      this.listArr = this.listArr.filter(item => {
        return item.id !== id;
      });
    });

    this.bus.$on("chenge", (id, checked) => {
      this.listArr.forEach(item => {
        if (item.id === id) {
          item.checked = checked;
        }
      });
    });
  }
};
</script>

<style scoped>
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
