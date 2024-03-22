<script setup>
import { reactive, defineEmits } from "vue";
import TodoButton from "@/components/TodoButton/index.vue";

const todoState = reactive({
  todo: "",
  errMsg: "",
});

const emit = defineEmits(["create-todo"]);

const createTodo = () => {
  if (todoState.todo.trim() === "") {
    todoState.errMsg = "Please enter a valid input.";
    return;
  }

  emit("create-todo", todoState.todo);

  todoState.errMsg = "";
  todoState.todo = "";
};
</script>

<template>
  <div class="input-wrapper test" :class="todoState.errMsg && 'input-err'">
    <input
      type="text"
      placeholder="Enter your Todo.."
      v-model="todoState.todo"
      :class="todoState.errMsg && 'input-err'"
    />

    <TodoButton @click="createTodo()" />
  </div>
  <p v-if="todoState.errMsg" class="err-msg">{{ todoState.errMsg }}</p>
</template>

<style lang="scss">
.err-msg {
  color: crimson;
  font-weight: 300;
  margin-top: 0.3rem;
  animation: up 0.3s forwards;
}

@keyframes up {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.input-wrapper {
  border: 2px solid #2b8b61;
  width: 100%;
  display: flex;
  border-radius: 0.3rem;
  overflow: hidden;
  box-shadow: 0 0 5px 1px rgba($color: #000000, $alpha: 0.1);

  &.input-err {
    border-color: crimson;
    transition: 100ms;
    box-shadow: 0 0 5px 1px rgba($color: crimson, $alpha: 0.1);
  }

  input {
    border: 1px solid transparent;
    flex: 1;
    height: 100%;
    padding: 0.5rem 0.5rem;
    color: #2b8b61;
    font-weight: 500;
    letter-spacing: 0.2px;
    border-radius: 0.2rem;
    border-top-right-radius: 0;
    border-bottom-right-radius: 0;
    transition: all 0.2s ease;

    &::placeholder {
      font-weight: normal;
      color: #7e9a8e;
    }

    &:focus {
      border-color: #2b8b61;
      outline: none;
    }

    &.input-err {
      &:focus {
        border-color: crimson;
      }
    }
  }
}
</style>
