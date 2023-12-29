<script setup>
import { Icon } from "@iconify/vue";
import { ref, computed } from "vue";
import { uid } from "uid";

import TodoCreator from "@/components/TodoCreator.vue";
import TodoItem from "@/components/TodoItem.vue";

const todoList = ref([]);

const createTodo = (todo) => {
  // This is perfectly fine, but the sample course asking to use the {uid} from the 'vue' package
  // todoList.value.push({
  //   id: todoList.value.length + 1,
  //   title: todo,
  //   completed: false,
  // });

  console.log("What are you??", todo);
  //  console.log(todo);

  todoList.value.push({
    id: uid(), // this UID is really cool, it generates a unique ID for each todo
    todo, // interesting enough, title and value can have this shortcut
    isCompleted: null,
    isEditing: null,
  });
  console.log(todoList.value);
};
</script>

<template>
  <main>
    <h1>Create ToDo</h1>
    <!-- We are adding the function above to this component -->
    <TodoCreator @create-todo="createTodo()" />
    <!-- This ul makes the item going down instead of side by side -->
    <ul>
      <!-- <TodoItem v-for="todo in todoList" /> -->
    </ul>
  </main>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
}
</style>
```
