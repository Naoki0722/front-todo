<template>
  <div class="input-area">
    <input type="text" class="form-area" v-model="message">
    <AddButton :addMessage="message" @clearText="clearText"></AddButton>
  </div>
</template>

<script>
import AddButton from "../components/AddButton.vue"
export default {
  data() {
    return {
      message: "",
    }
  },
  components: {
    AddButton
  },
  methods: {
    clearText() {
      this.message = "";
      this.$emit('add');
    }
  }
}
</script>

<style scoped>
.input-area {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.form-area {
  width: 70%;
  height: 30px;
  margin: 2% 0 2%;
  border: 1px solid rgb(195, 195, 195);
  border-radius: 5px;
}
</style>