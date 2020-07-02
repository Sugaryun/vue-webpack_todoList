<template>
  <div class="todo-helper">
    <span class="left">{{ unfinishedTodosLength }} items left</span>
    <span class="todo-tabs">
      <span
        v-for="state in states"
        :key="state"
        :class="['tab-state', filter === state ? 'active' : '']"
        @click="toggleFilter(state)"
        >{{ state }}
      </span>
    </span>
    <span 
    class="clearAllCompleted"
    @click="clearAllCompleted">Clear completed</span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      states: ["all", "active", "completed"],
    };
  },
  computed: {
    unfinishedTodosLength() {
      return this.todos.filter((todo) => !todo.completed).length;
    },
  },
  props: {
    filter: {
      type: String,
      required: true,
    },
    todos: {
      type: Array,
      required: true,
    },
  },

  methods: {
    toggleFilter(state) {
      this.$emit('toggleFilter', state)
    },
    clearAllCompleted() {
      this.$emit('clearAllCompleted')
    }
  },
};
</script>

<style lang="stylus">
.todo-helper {
    width 100%
    height 28px
    background-color #dcddf3
    display flex
    justify-content space-around
    align-items center
    color black
    font-weight 300
}
.todo-tabs {
    width 150px
    display flex
    justify-content space-between
}
.todo-tabs .tab-state {
    display block
    text-align center
    width 100%
    height 20px
}
.todo-tabs .active {
  border 2px solid #ff7f81
  border-radius 10px
}
</style>
