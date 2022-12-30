<template>
  <div id="app">
    <div class="inner">
      <TodoHeader></TodoHeader>
      <TodoInput v-on:addTodo="addTodo"></TodoInput>
      <TodoList v-bind:propsdata="todoItems" @removeTodo="removeItem"></TodoList>
      <!-- v-bind:프롭스속성이름="상위텀포넌트의 데이타이름" 상위에서하위로 전달 -->
      <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
      <!-- removeAll이 발생했을때 clearAll이 실행 -->
    </div>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  //name: "App",
  data() {
    return { todoItems: [] }; //스토리지 내용을 집어넣을 빈배열
  },

  components: {
    TodoHeader: TodoHeader,
    TodoInput: TodoInput,
    TodoList: TodoList,
    TodoFooter: TodoFooter,
  },
  //새로 인식할때 로컬스토리지에 남아있는 내용으로 배열을 만들어준다
  created: function () {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  methods: {
    addTodo(todoItem) {
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    clearAll() {
      localStorage.clear(); //localStorage에서만 삭제
      this.todoItems = []; //배열 데이타를 비워줌
    },
    removeItem(todoItem, index) {
      localStorage.removeItem(todoItem); //로컬스토리지에서 삭제
      this.todoItems.splice(index, 1); //배열에서 삭제
    },
  },
};
</script>

<style>
@font-face {
    font-family: 'IBMPlexSansKR-Light';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_20-07@1.0/IBMPlexSansKR-Light.woff') format('woff');
    font-weight: 300;
    font-style: normal;
}

@font-face {
    font-family: 'IBMPlexSansKR-Regular';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_20-07@1.0/IBMPlexSansKR-Regular.woff') format('woff');
    font-weight: 400;
    font-style: normal;
}

@font-face {
    font-family: 'IBMPlexSansKR-Bold';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_20-07@1.0/IBMPlexSansKR-Bold.woff') format('woff');
    font-weight: 600;
    font-style: normal;
}

@font-face {
    font-family: 'yg-jalnan';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_four@1.2/JalnanOTF00.woff') format('woff');
    font-weight: normal;
    font-style: normal;
}
.shadow {
  box-shadow: 0 10px 10px rgba(0, 0, 0, 0.1);
}

body{
  margin: 0;
  padding: 0;
  width:100%;
  height:100%;
  background-image: linear-gradient(to top, #a8edea 0%, #fed6e3 100%);
}

#app {
  font-family: "IBMPlexSansKR-Regular", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 640px;
  min-width: 320px;
  height: 100vh;
  display: table;
  width: 100%;
}

.inner{
  display: table-cell;
  vertical-align: middle;
}
</style>
