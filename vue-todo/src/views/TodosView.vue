<script setup>
import { ref, watch, onMounted, computed } from "vue";
import { uid } from "uid";
import { Icon } from "@iconify/vue";
import TodoCreator from "@/components/TodoCreator/index.vue";
import TodoList from "@/components/TodoList/index.vue";

const todoList = ref([]);

watch(
  todoList,
  () => {
    setTodoListToLocalStorge();
  },
  {
    deep: true,
  }
);

const todoCompleted = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted);
});

const getTodoListFromLocalStorage = () => {
  const storedTodoList = localStorage.getItem("todoList");
  const parsedTodoList = JSON.parse(storedTodoList);

  if (parsedTodoList) {
    todoList.value = parsedTodoList;
  }
};

onMounted(() => {
  getTodoListFromLocalStorage();
});

const setTodoListToLocalStorge = () => {
  const stringifiedTodoList = JSON.stringify(todoList.value);
  localStorage.setItem("todoList", stringifiedTodoList);
};

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
};

const toggleCompleteTodo = (todoId) => {
  const selectedTodo = todoList.value.find((todo) => todo.id === todoId);
  selectedTodo.isCompleted = !selectedTodo.isCompleted;
};

const toggleTodoEdit = (todoId) => {
  const selectedTodo = todoList.value.find((todo) => todo.id === todoId);
  selectedTodo.isEditing = !selectedTodo.isEditing;
};

const todoUpdate = (todoId, newVal) => {
  const selectedTodo = todoList.value.find((todo) => todo.id === todoId);
  selectedTodo.todo = newVal;
};

const todoDelete = (todoId) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== todoId);
};
</script>

<template>
  <main>
    <div class="container">
      <h1>Create Todo</h1>
      <TodoCreator @create-todo="createTodo" />
      <TodoList
        v-if="todoList.length !== 0"
        :todoList="todoList"
        @toggle-complete="toggleCompleteTodo"
        @todo-edit="toggleTodoEdit"
        @todo-update="todoUpdate"
        @todo-delete="todoDelete"
      />
      <p v-else class="no-todos">
        <Icon icon="noto-v1:sad-but-relieved-face" width="22" />
        <span>You have no todo's to complete! Add one.</span>
      </p>
      <p v-if="todoCompleted && todoList.length !== 0" class="todos-completed">
        <Icon icon="noto-v1:party-popper" width="22" />
        <span>All todos are Done.</span>
      </p>
    </div>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 4rem 2rem;

  .container {
    max-width: 30rem;
    width: 100%;
    text-align: center;

    h1 {
      margin-bottom: 1rem;
    }

    .todos-completed {
      margin-top: 2rem;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 0.5rem;

      color: #41b080;
      animation: fade-up 200ms ease forwards;

      @keyframes fade-up {
        from {
          opacity: 0;
          transform: translateY(0.3rem);
        }
        to {
          opacity: 1;
          transform: translateY(0);
        }
      }
    }

    .no-todos {
      margin-top: 2rem;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 0.5rem;
      color: #3d3d3d;
    }
  }
}
</style>
