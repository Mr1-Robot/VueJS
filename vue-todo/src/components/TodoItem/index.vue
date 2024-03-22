<script setup>
import { defineProps, defineEmits } from "vue";
import { Icon } from "@iconify/vue";

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits([
  "toggle-complete",
  "todo-edit",
  "todo-update",
  "todo-delete",
]);
</script>

<template>
  <li>
    <input
      type="checkbox"
      :checked="props.todo.isCompleted"
      @input="$emit('toggle-complete', props.todo.id)"
    />
    <div class="title">
      <input
        v-if="props.todo.isEditing"
        type="text"
        :value="props.todo.todo"
        @input="$emit('todo-update', props.todo.id, $event.target.value)"
      />
      <h4 v-else :class="props.todo.isCompleted && 'completed-todo'">
        {{ props.todo.todo }}
      </h4>
    </div>
    <div class="actions">
      <Icon
        v-if="props.todo.isEditing"
        icon="ph:check-circle"
        color="#2b8b61"
        width="22"
        class="icon"
        @click="$emit('todo-edit', props.todo.id)"
      />
      <Icon
        v-else
        @click="$emit('todo-edit', props.todo.id)"
        icon="ph:pencil"
        color="#6c7a73"
        width="22"
        class="icon"
      />
      <Icon
        @click="$emit('todo-delete', props.todo.id)"
        icon="ph:trash"
        color="#f95e5e"
        width="22"
        class="icon"
      />
    </div>
  </li>
</template>

<style lang="scss" scoped>
li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 2rem;
  border-radius: 0.5rem;
  box-shadow: 0 4px 4px -1px rgba($color: #00000035, $alpha: 0.1);
  background-color: #f1f1f1;
  padding: 1rem;
  animation: fade 0.2s ease forwards;

  h4 {
    text-align: left;

    &.completed-todo {
      text-decoration: line-through;
    }
  }

  input[type="checkbox"] {
    appearance: none;
    width: 1.2rem;
    height: 1.2rem;
    border-radius: 50%;
    background-color: #fff;
    box-shadow: 0 4px 6px -1px rgba($color: #000000, $alpha: 0.1);

    &:checked {
      background-color: #41b080;
    }
  }

  .title {
    flex: 1;
    input[type="text"] {
      border: 1px solid #41b080;
      padding: 0.1rem 0.3rem;
      border-radius: 0.2rem;
      width: 100%;
      outline: 1px solid transparent;
      transition: 200ms ease;

      &:focus {
        outline-color: #41b080;
      }
    }
  }

  .actions {
    opacity: 0;
    visibility: hidden;
    transition: 200ms ease;
    display: flex;
    align-items: center;
    gap: 1rem;

    .icon {
      cursor: pointer;
    }
  }

  &:hover .actions {
    opacity: 1;
    visibility: visible;
  }
}

@keyframes fade {
  from {
    opacity: 0;
    transform: translateY(0.2rem);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
