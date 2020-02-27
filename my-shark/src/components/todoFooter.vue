<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" />
    </label>
    <span>
      <span>已完成0</span>/全部2
    </span>
    <button class="btn btn-danger" @clear="clear">清除已完成任务</button>
  </div>
</template>
<script>
export default {
  name: "todoFooter",
  props: {
    listArr: Array
  },
  computed: {
    checkAll() {
      let flag = this.computedCount !== 0 && this.listArr.length !== 0;
      return this.computedCount === this.listArr.length && flag;
    },
    computedCount() {
      return this.listArr.reduce((adder, item) => {
        return adder + (item.checked ? 1 : 0);
      }, 0);
    }
  },
  methods: {
    clear() {
      this.$emit("clear");
    }
  }
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
