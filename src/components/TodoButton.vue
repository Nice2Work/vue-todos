<script setup></script>

<template>
  <!-- The slot is like a placeholder for text or other components, and can be addressed like = name='myID' 
it can also have a fallback content, so when the slot is empty it will show what is here under defined-->
  <button><slot>Create</slot></button>
</template>

<style lang="scss" scoped>
button {
  padding: 8px 16px;
  border: none;
}
</style>
