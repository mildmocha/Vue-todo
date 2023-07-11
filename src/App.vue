<script setup>
import { ref, watch, onMounted } from 'vue';

const todos = ref([]);
const name = ref('');

const input_content = ref('')//입력값
const input_category = ref(null);

const addTodo = () =>{
  if (input_content.value.trim() === '' || input_category.value === null ){ 

  return

}
  todos.value.push({
       content: input_content.value,
       category: input_category.value,
      createAt: new Date().getTime(),
      done:false,
      editable:false
     })
    //입력 후 초기화
    input_content.value = '';
    input_category.value= null;
  }





    //이름입력하는 것을 인지하고 로컬스토리지에 저장

watch(name, (newName) => {
  localStorage.setItem('name', newName)
})
//todo 변화 감지 로컬스토리지 업데이트
watch(todos, (newVal)=>{
  localStorage.setItem('todos',JSON.stringify(newVal))
},{deep:true})


//로컬스토리지 불러오기
onMounted(() => {
  name.value = localStorage.getItem('name') || '';
})

</script>

<template>
  <main class="app">
    <section class="greeting">
      <h1 class="title">
        whatsup
        <input type="text" placeholder="name here" v-model="name">

      </h1>

    </section>

    <section class="create-todo" v-on:submit.prevent="addTodo">
      <h2> create-todo</h2>
      <form id="new-todo-form">
        <h4> whats on ur todo list </h4>
        <input type="text" id="content" placeholder="e.g 포트폴리오 마무리"
        v-model="input_content"
        >
        {{ input_content }}
        <div class="options">
          <label>

            <input type="radio" name="category" id="category1" value="business" v-model="input_category">
            <span class="bubble business"></span>
            <div>business</div>
          </label>
          <label>
            <input type="radio" name="category" id="category2" value="personal" v-model="input_category">
            <span class="bubble personal"></span>
            <div>personal</div>
          </label>
        </div>
    <!--    {{ input_category }}-->

        <input type="submit" value="Add todo">

      </form>
    </section>

    <section class="todo-list">
      <div class="todo-item">
        <div>
          <label for="">
            <input type="checkBox">
            <span class="personal"></span>
          </label>
          <div class="todo-content">
            <input type="text" name="" id="" v-model="input_content">
          </div>
          <div class="actions">
            <button class="delete" @click=""></button>
          </div> 
        </div>
      </div>
    </section>
  </main>
</template>

