<template>
  <section class="real-app">
    <input
      type="text"
      class="add-input"
      placeholder="接下来要做什么？"
      autofocus="autufocus"
      @keyup.enter="addTodo"
    />
    <item 
    v-for="todo in filteredTodos"
    :key="todo.id"
    :todo="todo"
    @dev="deleteTodo"
    />
    <tabs 
    :filter="filter"
    :todos="todos"
    @toggleFilter="toggleFilter"
    @clearAllCompleted="clearAllCompleted"
    />
  </section>
</template>

<script>
import Item from "./item.vue";
import Tabs from "./tabs.vue";
let id = 0

export default {
  data() {
    return {
      todos: [],
      filter: "all",
    };
  },
  components: {
    Item,
    Tabs,
  },
  computed: {
    filteredTodos() {
      if(this.filter=='all') {
        return this.todos
      }
      const completed = this.filter === 'completed'
      return this.todos.filter(todo => completed===todo.completed)
    }
  },
  methods: {
    addTodo(e) {
      // console.log(e.target)
      this.todos.unshift({
        id: id++,
        content: e.target.value,
        completed: false
      })
      e.target.value = ''
    },

    deleteTodo(id) {
      () => {console.log(1)}
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1)
    },

    toggleFilter(state) {
      this.filter = state
    },
    clearAllCompleted() {
      this.todos = this.todos.filter(todo => !todo.completed)
    }
  },
};
</script>

<style lang="stylus">
.real-app{
  margin 0 auto
  width 600px
  box-shadow 0 0 5px #666
}
.add-input {
  width 100%
  font-size 24px
  font-family inherit
  font-weight inherit
  line-height 1.4em
  border 0
  outline none
  color inherit
  box-sizing border-box
  padding 16px
  font-smoothing antialiased
  border none
}
</style>
