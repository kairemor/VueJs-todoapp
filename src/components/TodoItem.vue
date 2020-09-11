<template>
  <div class="todo-item" v-bind:class="{'is-completed':todo.completed}">
    <p>
      <input type="checkbox" v-on:change="markComplete" />
      {{todo.title}}
      <button @click="$emit('del-todo', todo._id)" class="del">x</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    }
  }
};
</script>

<style scoped>
.todo-item {
  background: #e4efee;
  padding: 10px;
  border-bottom: 1px #ddd dotted;
}
.is-completed {
  text-decoration: line-through;
}
.del {
  float: right;
  background-color: red;
  border-radius: 100%;
  width: 30px;
  height: 30px;
}
</style>

