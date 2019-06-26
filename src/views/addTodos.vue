<template>
  <header class="header">
    <h1>todos</h1>
    <input
      class="new-todo"
      placeholder="What needs to be done?"
      autofocus
      v-model="msg"
      @keyup.enter="add"
    >
  </header>
</template>
<script>
export default {
  data() {
    return {
      msg: ""
    };
  },
  methods: {
    add() {
      if (this.msg.trim() == "") {
        return;
      }
      this.$emit("add", this.msg);
      // console.log(this.msg);
      this.msg = "";
    }
  }
};
</script>

