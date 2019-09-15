<template>
  <div id="app">
    <h1>Vue.js SHOPPING LIST</h1>
    <div class="container">

      <section>
         <div class="row justify-content-center">
           <input class="input-box" v-model="inputField" v-on:keyup.enter="addTodo" placeholder="Add new item" />
           <button @click="addTodo" class="btn btn-secondary">Add Todo</button>
        </div>
      </section>

       <section class="container">
          <div class="row">
             <div class="offset-md-3 col-md-6 mt-3">
                <ul class="list-group justify-content-center">
                   <li class="row list-group-item border mt-2" v-for="todo in todoList">
                      <div class="row align-items-center">
                        <input type="checkbox" v-on:change="toggle(todo)" v-bind:checked="todo.complete" class="col-sm-1 border border-danger">
                        <del v-if="todo.complete" class="col-sm-8">
                           <h5>{{ todo.name }}</h5>
                        </del>
                        <span v-else class="col-sm-8">
                           <h5>{{ todo.name }}</h5>
                        </span>
                        <span @click="deleteTodo(todo)" class="offset-sm-1 col-sm-2 delete text-right">X</span>
                      </div>
                   </li>
                </ul>
             </div>
          </div>
       </section>

    </div>

  </div>
</template>

<script>
import Vue from 'vue';
import BootstrapVue from 'bootstrap-vue';
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

import general from './components/general';

export default {
  name: 'app',
  components: {
     general
 },
  methods: {
    addTodo: function(todo) {
      todo = this.inputField;
      this.todoList.push({name: todo, complete: false});
      this.inputField = '';
   },
   deleteTodo: function(todo) {
      var index = this.todoList.indexOf(todo);
      this.todoList.splice(index, 1);
   },
   toggle: function(todo) {
      todo.complete = !todo.complete;
   }
 },
  data () {
    return {
      inputField: '',
      todoList: []
    }
  }
}
</script>

<style>
#app {
  font-family: Arial;
  text-align: center;
  margin: 0px;
  padding: 0px;
  min-width: 100vw;
  min-height: 100vh;
  background-image: url("./assets/background.jpg");
}

h1 {
  font-family: Goudy Old Style;
  color: white;
}

.input-box {
    margin-right: 10px;
    width: 300px;
    text-align: center;
}

h5 {
   margin-bottom: 0px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

.delete {
   cursor: pointer;
}

.delete:hover {
   color: #999999;
}
</style>
