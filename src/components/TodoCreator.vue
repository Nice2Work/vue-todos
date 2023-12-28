<script setup>
// this below is NOT reactive and will not change when changing the input field
// const todo = "testing";

// this below is reactive and will change when changing the input field
import { ref, defineEmits, reactive } from "vue";

// ********* This below works fine, but we are using the 'reactive method' below *********
// const todo = ref("");

const emit = defineEmits(["create-todo"]); // not sure why??

// console.log(todo.value);

const createTodo = () => {
  console.log(todoState.todo);
  emit("create-todo", todoState.todo); // each time we click it will EMIT the value of the input field
};

// here we use an object unlike in todoView we have an array
const todoState = reactive({
  todo: "",
  invalid: false,
  errMsg: "",
});

console.log(todoState.todo);
</script>

<template>
  <div class="input-wrap">
    <!-- Here we have a regular reactive method -->
    <!-- <input
      type="text"
      placeholder="Enter a new todo"
      v-model="todo"
      @keyup.enter="addTodo"
    /> -->
    <!-- Here we have a reactive method with the .value property -->
    <input
      type="text"
      placeholder="Enter a new todo"
      v-model="todoState.todo"
    />

    <button @click="createTodo" value="create">Create</button>
  </div>
  <p>{{ todoState.todo }}</p>
  <!-- <p>{{ todo }}</p> -->
</template>

<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;

  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }

  input {
    width: 100%;
    padding: 8px 6px;
    border: none;

    &:focus {
      outline: none;
    }
  }

  button {
    padding: 8px 16px;
    border: none;
  }
}
</style>
