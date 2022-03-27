<template>
  <div>
    <input v-model="newTodo" />
    <button @click="addNewTodo">add</button>
    <hr style="margin-top: 20px; margin-bottom: 20px" />

    <div v-if="todos.length > 0">
      <ul v-for="todo in todos" :key="todo.id">
        <li @click="statusChange(todo)" :class="`${todo.status ? 'liClass done' : 'liClass'}`">
          {{ todo.title }}
        </li>
      </ul>
    </div>
    <div v-else>there is not any todo</div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      newTodo: "",
      todos: [],
    };
  },
  methods: {
    addNewTodo() {
      let Todo = {
        id: new Date().getTime(),
        title: this.newTodo,
        status: false,
      };

      this.todos.push(Todo);

      this.newTodo = "";
    },
    statusChange (todo) {
       this.todos = this.todos.map(item => {
         if (item.id === todo.id) {
           item.status = !item.status
         }
         return item
       })
    }
  },
};
</script>

<style>
.liClass {
  color: blue;
  cursor: pointer;
}
.done {
  color: green;
}
</style>

