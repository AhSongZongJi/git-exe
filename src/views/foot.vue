<template>
  <footer class="footer" v-show="todoList.length">
    <!-- This should be `0 items left` by default -->
    <span class="todo-count">
      <strong>{{length}}</strong> item left
    </span>
    <!-- Remove this if you don't implement routing -->
    <ul class="filters">
      <li>
        <router-link to="/" active-class="selected" exact>All</router-link>
      </li>
      <li>
        <router-link to="/active" active-class="selected">Active</router-link>
      </li>
      <li>
        <router-link to="/completed" active-class="selected">Completed</router-link>
      </li>
    </ul>

    <button
      class="clear-completed"
      @click="clear"
      v-show="todoList.some( v => v.isShow)"
    >Clear completed</button>
  </footer>
</template>
<script>
export default {
  data() {
    return {
      btn: "all"
    };
  },
  props: ["todoList"],
  methods: {
    clear() {
      this.$emit("clear", "1");
    },
    btnTodo() {
      this.btn = this.$route.path;
    }
  },
  computed: {
    length() {
      return this.todoList.filter(v => !v.isShow).length;
    }
  }
};
</script>

