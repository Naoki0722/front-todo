<template>
  <div class="container">
    <div class="home">
        <h2>Todo List</h2>
      <div class="input-area">
        <input type="text" class="form-area" v-model="message">
        <button class="add-button" @click="addList">追加</button>
      </div>
      <div class="todo-list" v-for="(data,index) in lists" :key="index">
        <input type="text" v-model="data.list">
        <div class="list-button-area">
          <button
            class="update-button"
            @click="updateList(data.id,data.list)"
          >更新</button>
          <button
            class="delete-button"
            @click="deleteList(data.id)"
          >削除</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      message: "",
      lists: ""
    }
  },
  created() {
    //初回読み込みでapiよりデータ取得
    this.getLists();
  },
  methods: {
    async getLists() {
      let todoLists;
      await axios.get('https://warm-sea-73575.herokuapp.com/api/todos/')
      .then((response) => {
        todoLists = response.data.data;
        console.log(response);
      })
      .catch((error) => {
        console.log(error);
      });
      this.lists = todoLists;
    },
    addList() {
      axios.post('https://warm-sea-73575.herokuapp.com/api/todos/', {
        list: this.message
      })
      .then((response) => {
        console.log(response);
        this.getLists();
        this.message = "";
      })
      .catch((error) => {
        console.log(error);
      });
    },
    updateList(id,todo) {
      axios.put(`https://warm-sea-73575.herokuapp.com/api/todos/${id}`, {
        list: todo
      })
      .then((response) => {
        console.log(response);
        this.getLists();
      })
      .catch((error) => {
        console.log(error);
      });
    },
    deleteList(id) {
      axios.delete(`https://warm-sea-73575.herokuapp.com/api/todos/${id}`, {
        data: {
          id: id
        }
      })
      .then((response) => {
        console.log(response);
        this.getLists();
      })
      .catch((error) => {
        console.log(error);
      });
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

.todo-list {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.todo-list input {
  width: 35%;
  height: 30px;
  margin: 0.5% 0 0.5%;
  border: 1px solid rgb(195, 195, 195);
  border-radius: 5px;
}
.update-button {
  padding: 5px 13px;
  margin-right: 10px;
  color: #FA9770;
  font-weight: bold;
  border: 2px solid #FA9770;
  background-color: white;
  border-radius: 5px;
  transition-duration: 0.5s;
}
.update-button:hover {
  background-color: #FA9770;
  cursor: pointer;
  color: white;
}

.delete-button {
  padding: 5px 13px;
  margin-right: 30px;
  color: #71FADC;
  font-weight: bold;
  border: 2px solid #71FADC;
  background-color: white;
  border-radius: 5px;
  transition-duration: 0.5s;
}

.delete-button:hover {
  background-color: #71FADC;
  cursor: pointer;
  color: white;
}
</style>