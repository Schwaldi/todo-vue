<template>
  <div class="bg-white text-black w-1/2 m-auto mt-12 rounded-xl drop-shadow-2xl">
    <div class="text-center border-b border-slate-75 py-4">
      <h1 class="text-3xl py-4">My Todos</h1>
      <p class="text-xl" v-if="openTodos.length > 0">
        open Todos:{{ openTodos.length }}
      </p>
      <p class="text-xl" v-else>
        There are no Todos, congratulation!
      </p>
      <div class="mt-4 px-6">
        <input type="test" class="py-2 w-2/4 text-black border border-slate-75 rounded-md" v-model="newTodo"/>
        <button class="bg-sky-500 text-white py-2 ml-4 w-1/4 rounded-md" @click="addTodo">Add Todo</button>
      </div>
    </div>
    <div v-for="(todo, index) in todos" :key="todo.todo">
      <Todo 
        :todoprop="todo" 
        :todoindex="index" 
        @toggledone-index="toggleDone"
        @removetodo-index="deleteTodo"
      />
    </div>
    <div class="text-center border-t border-slate-75 py-8"> 
      <p class="text-md">
        “My mother always used to say: The older you get, the better you get, unless you’re a banana.” <br/>
        — Rose (Betty White), The Golden Girls —
      </p>
    </div>  
  </div>
</template>

<script>
import Todo from './components/Todo.vue'

export default {
  name: 'App',
  data() {
    return {
      newTodo: "",
      todos: [],
    };
  },
  methods: {
    toggleDone(index) {
      this.todos[index].done =!this.todos[index].done;
      this.storeTodos();
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
      this.storeTodos();
    },
    addTodo() {
      if(this.newTodo.trim() === "") {
        return;
      }
      this.todos.push({todo: this.newTodo, done: false });
      this.storeTodos();
    },
    storeTodos() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
  mounted () {
    let data = localStorage.getItem("todos");
    if(data !== "" && data !=null) {
      this.todos = JSON.parse(data);
    } else {
      this.todos = [];
    }
  },
  computed: {
    openTodos (){
      const openTodos = this.todos.filter ((todo) => {
        return !todo.done;
      });
      return openTodos;
    },
  },
  components: {
    Todo,
  },
}
</script>