<template>
  <section class="main">
    <input id="toggle-all" class="toggle-all" type="checkbox">
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <!-- These are here just to show the structure of the list items -->
      <!-- List items should get the class `editing` when editing and `completed` when marked as completed -->
      <li
        :class="{completed : itme.isShow,editing : itme.id == dblId}"
        v-for="itme in btnData"
        :key="itme.id"
        @dblclick="dbtodo(itme.id)"
      >
        <div class="view">
          <input class="toggle" type="checkbox" v-model="itme.isShow">
          <label>{{itme.todo}}</label>
          <button class="destroy" @click="Delete(itme.id)"></button>
        </div>
        <input class="edit" v-model="itme.todo" @keyup.enter="isOk">
      </li>
    </ul>
  </section>
</template>
<script>
export default {
  data() {
    return {
      dblId: -1
    };
  },
  props: ["todoList"],
  methods: {
    Delete(id) {
      this.$emit("todoDele", id);
    },
    dbtodo(id) {
      this.dblId = id;
    },
    isOk() {
      this.dblId = "";
    }
  },
  computed:{
    btnData() {
      // return this.todoList.filter( v => {
      //     if(this.$route.path == '/'){
      //         return true
      //     } else if (this.$route.path == '/active'){
      //         return v.isShow == false
      //     } else if(this.$route.path == '/completed'){
      //         return v.isShow == true
      //     }

      // });
      // switch 的性能比 if 性能要高
      switch (this.$route.path) {
        case "/":
          return this.todoList;
        case "/active":
          return this.todoList.filter(v => !v.isShow)
        case "/completed":
          return this.todoList.filter(v => v.isShow)
      }
    }
  }
};
</script>


