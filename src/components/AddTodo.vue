<template>
  <div>
    <form @submit="addTodo" action>
      <input type="text" v-model="title" name="title" placeholder="Add somethings todo" />
      <input type="submit" value="Add" class="btn" />
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        title: this.title,
        completed: false
      };
      //   #send the new todo to parent
      this.$emit("add-todo", newTodo);
      this.title = "";
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
}

input [type="text"] {
  flex: 10;
  padding: 6px;
}
input [type="submit"] {
  flex: 2;
}
.btn {
  display: inline-block;
  border: none;
  background: rgba(1, 48, 255, 0.671);
  padding: 5px, 20px;
  cursor: pointer;
}
.btn:hover {
  background: rgba(1, 48, 255);
}
</style>
