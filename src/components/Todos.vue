<template>
  <div class="container">
    <h3>
      Todos
    </h3>
    <div class="legend">
      <span>Double click to mark as complete</span>
      <span>
        <span class="incomplete-box">
          = Incomplete
        </span>
      </span>
      <span>
        <span class="complete-box">
          = Complete
        </span>
      </span>
    </div>
    <div class="todos">
      <div
        v-for="todo in allTodos"
        :key="todo.id"
        class="todo"
        @dblclick="onUpdate(todo)"
        :class="{'is-complete':todo.completed}"
      >
        {{todo.title}}
        <i
          class="fas fa-trash-alt"
          @click="deleteTodo(todo.id)"
        >
        </i>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';

export default {
  name: 'Todos',
  computed: {
    ...mapGetters(['allTodos']),
  },
  methods: {
    ...mapActions(['fetchTodos', 'deleteTodo', 'updateTodo']),
    onUpdate(todoElement) {
      let { completed } = todoElement;
      completed = !completed;
      const updatedTodo = { ...todoElement, completed };
      console.log(updatedTodo);
      this.updateTodo(updatedTodo);
    },
  },
  created() {
    this.fetchTodos();
  },
};
</script>

<style lang="scss" scoped>
.legend {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1rem;
  .complete-box {
    display: inline-block;
    width: 10px;
    height: 10px;
    background: #35495e;
  }
  .incomplete-box {
    display: inline-block;
    width: 10px;
    height: 10px;
    background: #41b883;
  }
}

.todos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;

  .todo {
    border: 1px solid #ccc;
    background: #41b883;
    padding: 1rem;
    border-radius: 5px;
    text-align: center;
    position: relative;
    cursor: pointer;

    &.is-complete {
      background: #35495e;
      color: #fff;
    }

    i{
      position: absolute;
      bottom: 10px;
      right: 10px;
      color: white;
      cursor: pointer;
    }
  }
}
</style>
