<script setup>

import {ref,onMounted ,watch,computed} from 'vue'

const todo=ref([]);
const name=ref('');
const input_color=ref('');
const input_catagory=ref(null)
const input_price=ref()
const addTodo=()=>{
  console.log('todo array',todo)
  todo.value.push({
    color:input_color.value,
    name:name.value,
    catagory:input_catagory.value,
    price:input_price.value,  
  })
  input_color.value='';
  name.value='';
  input_catagory.value='';
  input_price.value=''
  console.log('add todo')
}
const deleteItem=(data)=>{
todo.value = todo.value.filter(t=>t !==data)
console.log(todo.value)
}
const todos_asc = computed(() => todo.value.sort((a,b) =>{
	return a.createdAt - b.createdAt
}))
watch(todo, (newVal) => {
	localStorage.setItem('todos', JSON.stringify(newVal))
}, {
	deep: true
})
onMounted(()=>{
  localStorage.getItem('todos') 
  todo.value = JSON.parse(localStorage.getItem('todos')) || []

})

</script>

<template>
  <div class="container  ">
  <form @submit.prevent="addTodo">
    <div>
            <label for="first_name" class="block m-3 text-md font-medium text-grB-lack-ay-900 dark:text-white">Product name</label>
            <input type="text" id="first_name" 
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg  w-full px-4 py-2 "
             placeholder="Product Name" 
             v-model="name"
             
           >
        </div>
       
        <div>
            <label for="first_name" class="block m-3 text-md font-medium text-grB-lack-ay-900 dark:text-white">Product Color</label>
            <input type="text" id="color" 
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg  w-full px-4 py-2 "
             placeholder="Product Color" 
           v-model="input_color"
          >
        </div>
        <div class="">
            <label for="first_name" class="block m-3 text-md font-medium text-grB-lack-ay-900 dark:text-white">Catagory</label>
         
           <div class="flex  justify-center">
            
          <p class="text-center">network</p> 
           <input type="radio" id="first_name" 
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg  w-full px-4 py-2 "
             placeholder="Product Name" 
           name="catagory"
           value="Network"
           v-model="input_catagory"
               > 
               <p>Software</p>
               <input type="radio" id="first_name" 
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg  w-full px-4 py-2 "
             placeholder="Product Name" 
           name="catagory"
           value="Software"
           v-model="input_catagory"

               ></div>
               <div>
        
            <label for="first_name" class="block m-3 text-md font-medium text-grB-lack-ay-900 dark:text-white">Product Price $</label>
            <input type="text" id="price" 
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg  w-full px-4 py-2 "
             placeholder="Product Price" 
           v-model="input_price"
           >
        </div>
        </div >
        <div class="mx-2 px-2 px-3 py-2 bg-zinc-600">        
          <input type="submit" value="Add todo" class=" btn mx-2 px-2 px-3 py-2 bg-zinc-600">
</div>
      </form>
<div class="relative overflow-x-auto shadow-md sm:rounded-lg text-center mt-5">
 
    <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
            <tr>
                <th scope="col" class="px-6 py-3">
                    Product name
                </th>
                <th scope="col" class="px-6 py-3">
                    Color
                </th>
                <th scope="col" class="px-6 py-3">
                    Category
                </th>
                <th scope="col" class="px-6 py-3">
                    Price
                </th>
                <th scope="col" class="px-6 py-3">
                    Action
                </th>
            </tr>
        </thead>
        <tbody :key="todoData.price" v-for="todoData in todo" >
         <tr>
                <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                 {{todoData.name}}
                </th>
                <td class="px-6 py-4">
                  {{ todoData.color }}
                </td>
                <td class="px-6 py-4">
              {{todoData.catagory}}
                </td>
                <td class="px-6 py-4">
                  {{ todoData.price}} $
                </td>
                <td class="px-6 py-4">
                      <i @click="deleteItem(todoData)" class="fas fa-times color-[#000]"></i>
                </td>
            </tr>
        </tbody>
    </table>
</div>

  </div>
 
</template>

<style scoped>
 .container{
  display: flex-col;
  justify-content: center;
  width:50%;
  align-items: center;
  margin:0 auto;
 }
 .btn{
  background-color:#176B87 ;
 color:#fff;
 border-radius: 5px;
 cursor: pointer;
 }
 .btn:hover{
  background: #fff;
  color: #176B87;
 }
</style>
