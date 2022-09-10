<template>
  <div 
    class="flex justify-between items-center py-3 px-8" 
    :class="{ 'bg-green-100':this.todo.done, 'bg-red-100': !todo.todo.done }"
  >
    <h1 class="cursor-pointer" @click="toggleTodo">{{ todo.todo }}</h1>
    <button class="text-white bg-red-500 py-1 px-2 rounded-md" @click="removeTodo">Delete Todo</button>
  </div>
</template>

<script>
export default {
  name: 'Todo-vue',
  props: ["todoprop","todoindex"],
  data() {
    return {
      todo: this.todoprop,
    }
  },
  methods: {
    toggleTodo() {
      this.$emit("toggledone-index", this.todoindex);
    },
    removeTodo() {
      this.$emit("removetodo-index", this.todoindex);
    },
  },
}
</script>
