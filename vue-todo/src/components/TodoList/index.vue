<script setup>
import { defineProps, defineEmits } from "vue";
import TodoItem from "@/components/TodoItem/index.vue";

const props = defineProps({
  todoList: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits([
  "toggle-complete",
  "todo-edit",
  "todo-update",
  "todo-delete",
]);

const emitTodoId = (todoId) => {
  emit("toggle-complete", todoId);
};

const emitTodoEdit = (todoId) => {
  emit("todo-edit", todoId);
};

const emitTodoUpdate = (todoId, newVal) => {
  emit("todo-update", todoId, newVal);
};

const emitTodoDelete = (todoId) => {
  emit("todo-delete", todoId);
};
</script>

<template>
  <div class="container">
    <h3>Todo's</h3>

    <ul class="list" v-if="todoList.length !== 0">
      <TodoItem
        v-for="todo in todoList"
        :key="todo.id"
        :todo="todo"
        @toggle-complete="emitTodoId"
        @todo-edit="emitTodoEdit"
        @todo-update="emitTodoUpdate"
        @todo-delete="emitTodoDelete"
      />
    </ul>
  </div>
</template>

<style lang="scss" scoped>
.container {
  margin-top: 3rem;

  h3 {
    margin-bottom: 2rem;
  }

  .list {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
}
</style>
