<script>
let id = 0

export default 
{
  data() 
  {
    return { 
      titleClass: 'title',
      message: 'Hello World',
      counter: 
      {
        count: 3
      },
      text1: '',
      text2: '',
      awesome: true,
      newTodo: '',
      hideCompleted: false,
      todos: [
        { id: id++, text: 'Learn HTML',done: false},
        { id: id++, text: 'Learn JavaScript',done: false},
        { id: id++, text: 'Learn Vue',done: false}
      ] // Todos list
    }
  }, // Data
  computed: 
  {
    filteredTodos() 
    {
      return this.hideCompleted ? this.todos.filter( t=> !t.done ) : this.todos
    }
  },
  methods: 
  {
    increment() 
    {
      this.counter.count++; // Update count variable
    },
    onInput(e)
    {
      this.text1 = e.target.value;
    },
    toggle() 
    {
      this.awesome = !this.awesome;
    },
    addTodo()
    {
      if(!(this.newTodo === "")) // Don't allow empty string
      {
        this.todos.push({id: id++, text: this.newTodo});
        this.newTodo='';
      }
    },
    removeTodo(todo)
    {
      let i = todo.id;

      // Remove element from the list
      this.todos.splice(todo.id,1); 

      // Update all element todo id's for all todo's after
      while(i < this.todos.length)
      {
        this.todos[i].id--;
        i++;
      }
      id--; // Update the id varaible
    }
    
  } // Methods
}
</script>

<template>
  <!-- Shorthand: ":class" -->
  <h1 v-bind:class="titleClass"> {{ message }} </h1>
   <!-- Shorthand: "@:click"  -->
  <button v-on:click="increment">Count is: {{counter.count}}</button> 
  <div></div>

  <input :value="text1" @input="onInput" placeholder="Text...">
  <p>{{ text1 }}</p>

  <!-- V-model automaticlaly syncs the input's value to it's state so 
  the onInput(e) methods is not needed anymore 
  (also works with checkboxes, radio buttons, and select dropdowns.) -->
  <input v-model="text2" placeholder="Text...">
  <p>{{ text2 }}</p>

  <!-- Toggle different states for headers -->
  <button @click="toggle"> Toggle </button>
  <h2 v-if="awesome">Vue is awesome!</h2>
  <h2 v-else>:(</h2>

  <!-- Create a Todo list that can be added to a removed from -->

  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>

  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">

      <input type="checkbox" v-model="todo.done">

      <span :class="{ done: todo.done }"> {{ todo.text }} </span>
      <!-- {{ todo.id }} -->
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed'}}
  </button>

</template>

<style>
.title {
  color: red;
}
.done {
  text-decoration: line-through;
}
</style>