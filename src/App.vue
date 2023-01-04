<script>
export default {
  data() {
    return { 
      titleClass: 'title',
      message: 'Hello World',
      counter: {
        count: 3
      },
      text1: '',
      text2: '',
      awesome: true
    }
  }, // Data
  methods: {
    increment() {
      this.counter.count++; // Update count variable
    },
    onInput(e)
    {
      this.text1 = e.target.value;
    },
    toggle()
    {
      this.awesome = !this.awesome;
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

  <button @click="toggle"> Toggle </button>
  <h2 v-if="awesome">Vue is awesome!</h2>
  <h2 v-else>:(</h2>

</template>

<style>
.title {
  color: red;
}
</style>