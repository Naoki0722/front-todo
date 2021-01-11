<template>
  <button class="add-button"  @click="addList">追加</button>
</template>

<script>
import axios from "axios";
export default {
  props: ["addMessage"],
  data() {
    return {
      
    }
  },
  methods: {
    addList() {
      axios.post('https://warm-sea-73575.herokuapp.com/api/todos', {
        list: this.addMessage
      })
      .then((response) => {
        console.log(response);
        this.$emit("clearText");
      })
      .catch((error) => {
        console.log(error);
      });
    }
  },
}
</script>

<style scoped>
.add-button {
  padding: 5px 13px;
  margin-right: 30px;
  color: #DC70FA;
  font-weight: bold;
  border: 2px solid #DC70FA;
  background-color: white;
  border-radius: 5px;
  transition-duration: 0.5s;
}
.add-button:hover {
  background-color: #DC70FA;
  cursor: pointer;
  color: white;
}
</style>