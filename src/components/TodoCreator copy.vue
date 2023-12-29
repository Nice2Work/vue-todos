<script setup>
// this below is NOT reactive and will not change when changing the input field
// const todo = "testing";

// this below is reactive and will change when changing the input field
import { ref, defineEmits, reactive } from "vue";
import TodoButton from "./TodoButton.vue";
import TodoItem from "./TodoButton.vue";
// ********* This below works fine, but we are using the 'reactive method' below *********
//const todo = ref("");

// here we use an object unlike in todoView we have an array
const todo = reactive({
  todo: "",
  invalid: false,
  errMsg: "",
});

const emit = defineEmits(["create-todo"]); // not sure why??

// console.log(todo.value);

const createTodo = () => {
  if (todo.todo === "") {
    todo.invalid = true;
    todo.errMsg = "Please enter a todo";
    return;
  }
  todo.errMsg = "";
  console.log("Are you here?", todo.todo);
  todo.invalid = false;
  emit("create-todo", todo.todo); // each time we click it will EMIT the value of the input field
  //todo.todo = "";
};

console.log(todo.todo);
</script>

<template>
  <div class="input-wrap" :class="{ 'input-err': todo.invalid }">
    <!-- Here we have a regular reactive method -->
    <!-- <input
      type="text"
      placeholder="Enter a new todo"
      v-model="todo"
      @keyup.enter="addTodo"
    /> -->
    <!-- Here we have a reactive method with the .value property -->
    <input type="text" placeholder="Enter a new todo" v-model="todo.todo" />
    <TodoButton @click="createTodo">
      <!-- a slot is like a placeholder and can have an ID, this way you can re-use this part over and over again-->
      Create Poes
    </TodoButton>
    <TodoItem />
    <!-- This works fine, but now we are learning about SLOTS -->
    <!-- <button @click="createTodo" value="create">Create</button> -->
  </div>
  <!-- <div v-if="todo.invalid === true" class="err-msg"> -->
  <!-- the v-show is FASTER as it is already in the DOM, and the visibility css is toggled, whereas v-if needs to be 
    created in the dome each time when it is toggled -->
  <div v-show="todo.invalid" class="err-msg">
    {{ todo.errMsg }}
  </div>
  <!-- <p>{{ todo.todo }}</p> -->
  <!-- <p>{{ todo }}</p> -->
</template>

<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;

  &.input-err {
    border-color: red;
  }

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

  //   button {
  //     padding: 8px 16px;
  //     border: none;
  //   }
}
.err-msg {
  margin-top: 6px;
  font-size: 12px;
  text-align: center;
  color: red;
}
</style>
