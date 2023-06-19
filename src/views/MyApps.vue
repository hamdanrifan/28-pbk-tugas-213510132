<template>
    <div class="todo-list">
     <h1>LIST KEGIATAN</h1>
     <form @submit.prevent="addTodo">
       <input type="text" v-model="newTodo" placeholder="Tambahkan Kegiatan Baru Anda">
       <button>Tambah</button>
     </form>
     <div class="filter-buttons">
       <a @click="updateActive('all')" :class="{ active: active === 'all' }">Semua</a>
       <a @click="updateActive('active')" :class="{ active: active === 'active' }">Sedang Dikerjakan</a>
       <a @click="updateActive('completed')" :class="{ active: active === 'completed' }">Sudah Selesai</a>
     </div>
     <ul>
       <li v-for="(todo, index) in filteredTodos" :key="index" :class="{ completed: todo.completed }">
         <input type="checkbox" v-model="todo.completed" @change="updateTodo" />
         <span>{{ todo.text }}</span>
         <div class="buttons">
           <button @click="removeTodo(index)">Hapus Tugas</button>
         </div>
       </li>
     </ul>
   </div>
 </template>
 
 <script>
 export default {
   data() {
     return {
       todos: [

       ],
       newTodo: '',
       filter: 'all',
       active: 'all'
     }
   },
   methods: {
     addTodo() {
       if (this.newTodo) {
         this.todos.push({
           text: this.newTodo,
           completed: false
         })
         this.newTodo = ''
       }
     },
     removeTodo(index) {
       this.todos.splice(index, 1)
     },
     updateTodo() {
       // Nothing to do here
     },
     updateActive(filter) {
       this.filter = filter;
       this.active = filter;
     }
   },
   computed: {
     filteredTodos() {
       if (this.filter === 'completed') {
         return this.todos.filter(todo => todo.completed)
       } else if (this.filter === 'active') {
         return this.todos.filter(todo => !todo.completed)
       } else {
         return this.todos
       }
     }
   }
 }
 </script>
 <style>
 h1{
   font-weight: bolder;
 }
 body{
   background-color: #e0e4cc;
 }
 .todo-list {
   margin: 20px auto;
   max-width: 600px;
   text-align: center;
 }
 form {
   margin: 20px 0;
   display: flex;
   justify-content: space-between;
 }
 input[type="text"] {
   padding: 10px;
   border: none;
   border-radius: 5px;
   box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.2);
   margin-right: 10px;
   width: 80%;
   background-color: #fff2bc;
   color: black ;
 }
 button {
   padding: 10px 20px;
   border: none;
   border-radius: 5px;
   background-color: #fff2bc;
   color: #151517;
   cursor: pointer;
   margin: 0 5px;
 }
 button:hover{
   background-color:#d83f75;
 }
 
 ::placeholder{
   color:black;
   opacity: 0.5;
 }
 ul {
   list-style: none;
   margin: 0;
   padding: 0;
 }
 li {
   display: flex;
   justify-content: space-between;
   align-items: center;
   padding: 10px;
   background-color: #fff2bc;
   margin-bottom: 10px;
   box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.2);
   border-radius: 5px;
   font-size:large;
 }
 .completed {
   text-decoration: line-through;
 }
 .filter-buttons {
   margin: 30px 0px;
 }
 input[type='checkbox']{
   content: "";
   display: flex;
   width: 25px;
   height: 25px;
   border: 2px solid #555555;
   border-radius: 3px;
   background-color: black;
 }
 
 
 
 </style>
 <style scoped>
 a{
   padding: 10px 20px;
   border: 3px solid #fff2bc;
   border-radius: 5px;
   background-color: #fff2bc;
   color: #050505;
   cursor: pointer;
   margin: 0px 5px;
   font-weight: bolder;
   box-sizing: border-box;
 }
 a.active{
     color: #141415  ;
     background-color: #8cd212;
     border: none;
     box-sizing: border-box
 }
 </style>