<template>
  <div class="container">
    <div class="home">
        <h2>Todo List</h2>
      <InputArea @add="clearText"></InputArea>
      <ListArea ref="child"></ListArea>
    </div>
  </div>
</template>

<script>
import InputArea from "../components/InputArea.vue"
import ListArea from "../components/ListArea.vue"
export default {
  components: {
    InputArea,
    ListArea,
  },
  methods: {
    clearText() {
      //ListAreaのメソッドを発火させる
      this.$refs.child.getLists();
    }
  }
  // watchやcomputedはdataプロパティーの加工や監視に使う。
  // watch: {
  //   listUpdate() {
  //     this.getLists();
  //   },
  //   listDelete() {
  //     this.getLists();
  //   }
  // }
  
}
</script>


<style scoped>
.container {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.home {
  width: 50%;
  background-color: white;
  border-radius: 20px;
  margin: 0 auto;
  padding-left: 40px;
}

.home h2 {
  font-size: 1.8rem;
  padding: 20px 0;
}
</style>