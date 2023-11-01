<script setup>
import { ref, onMounted , computed , watch } from 'vue'
const todos= ref([])
const name= ref('')

const input_content= ref('')

const addTodo= ()=>{

  if(input_content.value.trim() === '')  return

  todos.value.push({
    content: input_content.value,
    done: false
  })
  
}

const removeTodo = todo =>{

  todos.value=todos.value.filter(todo2 => todo2 !== todo)

}

watch(name , (newVal)=>{
  localStorage.setItem("name", newVal);
})



onMounted(()=>{
  name.value= localStorage.getItem("name") || ''
})



</script>

<template>


 <main class="app">
   <section class="greeting">
    <h2 class="title">
       Hey! , <input type="text" placeholder="Enter your name" v-model="name" />

    </h2>
   </section>
   <section class="create-todo">
     <h3>ADD SOME NEW TASKS</h3>
      <form @submit.prevent="addTodo">
        <input type="text"
         placeholder="e.g. Learn typescript" 
         v-model="input_content" />
       
        <input type="submit" value="Add Todo" />
      </form>
   </section>
   <section class="todo-list">
    <h3>TODO - LIST</h3>
    <div class="list">


      <div v-for="todo in todos" :class="`todo-item ${todo.done && 'done'}`">
          <label>
             <input type="checkbox" v-model="todo.done"/>
             <span class="bubble"></span>
          </label>

          <div class="todo-content">
            <input type="text" v-model="todo.content"/>
          </div>

          <div class="actions">
            <button class="delete" @click="removeTodo(todo)">Delete</button>
          </div>
      </div>
    </div>
   </section>
 </main>

  
 
</template>


