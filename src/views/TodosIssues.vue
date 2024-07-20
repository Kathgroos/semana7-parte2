<template>
    <div>
      <h1>TodosIssues</h1>
    <!-- Formulario para agregar una nueva tarea-->
      <form @submit.prevent="addTodo()">
        <el-input placeholder="todo" v-model="todo"></el-input>
      </form>
      <el-row :gutter="12">
        <!-- Área de visualización de tareas pendiente  -->
        <TodoItem v-for="(todo, index) in todos" :key="index" :index="index" :todo="todo" @remove-todo="removeTodo" />
        <!-- Área de visualización de problemas -->
      <TodoItem v-for="(issue, index) in issues" :key="index" :index="index" :todo="issue.title" @remove-todo="closeIssue" />
      </el-row>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import TodoItem from '@/components/TodoItem';
  
  const client = axios.create({
    baseURL: `${process.env.VUE_APP_GITHUB_ENDPOINT}`,
    headers: {
      'Authorization': `token ${process.env.VUE_APP_GITHUB_TOKEN}`,
      'Accept': 'application/vnd.github.v3+json',
      'Content-Type':'application/json',
    },
  })
  
  export default {
    name: 'TodosIssues',
    components: {
      TodoItem
    },
    data () {
      return {
        todo: '',
        todos: [], //Lista de todos los locales.
        issues: [] //Lista de issues obtenidos de Github.
      }
    },
    methods: {
    //Metodo para añadir una nueva tarea localmente.
      addTodo(){
        this.todos.push(this.todo);
        this.todo= '';
      },
      //Metodo para eliminar una tarea localmente.
      removeTodo(index){
        this.todos.splice(index, 1);
      },
      //Método para cerrar un issue en Github.
      closeIssue(index){
        const target = this.issues[index];
        client.patch(`/issues/${target.number}`,
            {
              state: 'closed'
            },
          )
          .then(() => {
           this.issues.splice(index, 1);
        })
      },
      //Método para obtener la lista de issues desde Github.
      getIssues() {
        client.get('issues')
          .then((res) => {
            this.issues = res.data
        })
      }
    },
    created() {
      this.getIssues();
    }
  }
  </script>