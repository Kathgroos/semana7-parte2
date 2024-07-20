<template>
    <div>
      <h1>TODO LIST</h1>
      <form @submit.prevent="addTodo">
        <!--<label for="todo">Lista de quehaceres</label>-->
        <div>
          <el-input v-model="todo" placeholder="Todo" />
          <!--<el-button type="primary" @click="addTodo">agregar</el-button>-->
        </div>
      </form>
  
      <el-row :gutter="12">
        <el-col :span="12" v-for="(todo, index) in todos" :key="index">
          <el-card class="box-card" shadow="hover">
            <el-row :gutter="12">
              <el-col :span="18">{{ todo }}</el-col>
              <el-col :span="4">
                <el-button @click="removeTodo(index)" icon="el-icon-check" type="success" circle></el-button>
              </el-col>
            </el-row>
          </el-card>
        </el-col>
      </el-row>
    </div>
  </template>
  
  <script>
  export default {
    name: "TodoList",
    data() {
      return {
        todo: "",
        todos: JSON.parse(localStorage.getItem('todos')) || [],
      };
    },
    methods: {
      addTodo() {
        this.todos.push(this.todo);
        localStorage.setItem('todos', JSON.stringify(this.todos));
        this.todo = "";
      },
      removeTodo(index) {
        this.todos.splice(index, 1);
        localStorage.setItem('todos', JSON.stringify(this.todos));
      },
    },
  };
  </script>