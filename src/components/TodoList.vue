<template>
  <div class="todo-list">
    <h2 class="title">Todo List</h2>
    <input
      type="text"
      class="input-new-item"
      v-on:keyup.enter="addNewItemToList"
    />
    <ul>
      <list-item
        v-for="(item, index) in list"
        :key="index"
        :index="index"
        :item="item"
        @delete-item="deleteItem"
        v-model="item.checked"
        class="item-style"
      />
    </ul>
  </div>
</template>

<script>
import ListItem from "./ListItem";
export default {
  name: "TodoList",
  components: {
    ListItem,
  },
  data() {
    return {
      list: [],
    };
  },
  created() {
    const itensInLocalStorage = JSON.parse(localStorage.getItem("list"));
    this.list = itensInLocalStorage ? itensInLocalStorage : [];
  },

  methods: {
    addNewItemToList(event) {
      const newItem = event.target.value;
      this.list.unshift({
        label: newItem,
        checked: false,
      });
      event.target.value = "";
    },
    deleteItem(index) {
      this.list.splice(index, 1);
    },
    updateLocalStorage() {
      localStorage.setItem("list", JSON.stringify(this.list));
      console.log(this.list)
    },
  },
  watch: {
    list() {
      this.updateLocalStorage();
    },
  },
};
</script>

<style scoped>
.todo-list {
  max-width: 500px;
  margin: auto;
  padding-top: 50px;
}
.input-new-item {
  width: 80%;
  height: 30px;
}
ul {
  list-style: none;
  padding: 0;
  width: 80%;
  margin: 20px auto;
  text-align: left;
}
.title{
  margin-bottom: 20px;
  color: #fff;
}
.item-style{
  background-color:rgb(66, 63, 209);
  background-color: #1B1F29;
  margin-bottom: 8px;
  padding: 10px 8px;
  border-radius: 4px;
  color: #ffff;
}
</style>
