
<template>
<div id="app-2">
  <div>{{msg}}</div>
  <span v-bind:title="message">
      Hover your mouse over me for a few seconds
      to see my dynamically bound title!
  </span>

  <p></p>
  <span v-if="seen">Now you see me</span>
  <button v-on:click="seen=!seen">you can seen: {{seen}}</button>
  <button @click="seen=!seen">Change it</button>

  <ol>
    <li v-for="todo in todos" v-bind:key="todo.id">
      {{ todo.text }}
    </li>
  </ol>

  <p>{{ rmsg }}</p>
  <button v-on:click="reverseMessage">Reverse Message</button>

  <p>{{ model }}</p>
  <input v-model="model">

  <ol>
    <!--
      Now we provide each todo-item with the todo object
      it's representing, so that its content can be dynamic.
      We also need to provide each component with a "key",
      which will be explained later.
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id">
    </todo-item>
  </ol>

  <!--HelloWorld></HelloWorld-->
</div>

</template>

<script>
// import HelloWorld from './HelloWorld.vue'
import Vue from 'vue'
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

export default {
  name: 'Test',
  data () {
    return {
      msg: 'Test Vue components!',
      message: 'You loaded this page on ' + new Date().toLocaleString(),
      seen: true,
      todos: [
        {id: 1, text: 'Learn JavaScript'},
        { id: 2, text: 'Learn Vue' },
        { id: 3, text: 'Build something awesome' }
      ],
      groceryList: [
        { id: 0, text: 'Vegetables' },
        { id: 1, text: 'Cheese' },
        { id: 2, text: 'Whatever else humans are supposed to eat' }
      ],
      rmsg: 'Hello vue.js!',
      model: 'Hello vue!'
    }
  },
  methods: {
    reverseMessage: function () {
      this.rmsg = this.rmsg.split('').reverse().join('')
    }
  }
  // components: { HelloWorld }
}
</script>
