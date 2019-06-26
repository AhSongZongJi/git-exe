<template>
  <div id="app">
    <section class="todoapp">
      <!-- 头部 -->
      <addtodo @add="add"></addtodo>
      <!-- 列表 -->
      <list :todoList="todoList" @todoDele="todoDele"></list>
      <!-- 底部 -->
      <foot :todoList="todoList" @clear="clearTodo"></foot>
    </section>
    <footer class="info">
      <p>Double-click to edit a todo</p>
      <!-- Remove the below line ↓ -->
      <p>
        Template by
        <a href="http://sindresorhus.com">Sindre Sorhus</a>
      </p>
      <!-- Change this out with your name and url ↓ -->
      <p>
        Created by
        <a href="http://todomvc.com">you</a>
      </p>
      <p>
        Part of
        <a href="http://todomvc.com">TodoMVC</a>
      </p>
    </footer>
    <!-- <router-view /> -->
  </div>
</template>

<script>
import addtodo from "./views/addTodos.vue";
import list from "./views/list.vue";
import foot from "./views/foot.vue";
export default {
  components: {
    addtodo,
    list,
    foot
  },
  data() {
    return {
      todoList: [
        { id: 1, todo: "锄禾日当午", isShow: false },
        { id: 2, todo: "汗滴禾下土", isShow: false }
      ]
    };
  },
  methods: {
    todoDele(id) {
      this.todoList = this.todoList.filter(v => v.id !== id);
    },
    add(value) {
      let temp = { id: +new Date(), todo: value, isShow: false };
      this.todoList.unshift(temp);
    },
    clearTodo(value) {
      console.log(value);
      this.todoList = this.todoList.filter(v => !v.isShow);
    }
  }
};
</script>
