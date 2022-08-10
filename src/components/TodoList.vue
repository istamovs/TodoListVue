<template>
  <div class="container todo-container">
    <div class="header">TODO - LIST</div>
    <div class="clear-all-button btn outlined" @click="clearAllMethod">Clear All</div>
    <div class="input-container">
      <input class="input-todo outlined" maxlength="45" placeholder="Start writing a task...." ref="inputTodo"/>
      <input type="submit" class="add-button btn outlined" value="Add" @click="addItemMethod"/>
    </div>
    <div class="items-container">
      <div class="item" v-for="(item, index) in items">
        <div class="item-text outlined">{{ item }}</div>
        <div class="item-edit btn outlined" @click="onShowDialog(index)">Edit</div>
        <div class="item-remove btn outlined" @click="removeItemMethod(index)">Remove</div>
      </div>
    </div>
  </div>
  <edit-dialog v-bind:show="showDialog" @close="showDialog = false" @accept="onDialogAccept"/>
</template>

<script>

import EditDialog from "./EditDialog.vue";

export default {
  name: "todo-list",
  components: {EditDialog},
  data() {
    return {
      items: [],
      showDialog: false,
      editingItemIndex: null
    }
  },
  methods: {
    addItemMethod() {
      if (!this.$refs.inputTodo.value) {
        alert('Task cannot be empty');
      } else {
        this.items.push(this.$refs.inputTodo.value)
      }
      this.$refs.inputTodo.value = '';
    },
    removeItemMethod(index) {
      this.items.splice(index, 1)
    },
    clearAllMethod() {
      this.items = []
    },
    onShowDialog(index) {
      this.editingItemIndex = index;
      this.showDialog = true;
    },
    onDialogAccept(value) {
      if (value && this.editingItemIndex !== null) {
        this.items.splice(this.editingItemIndex, 1, value)
      }
    }
  }
}

</script>

<style scoped>

.todo-container {
  height: auto;
  width: 650px;
  border: solid 2px black;
  display: flex;
  flex-direction: column;
}

.clear-all-button {
  margin-left: 20px;
  background: #d77272;
}

.header {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 10px;
}

.input-container {
  width: 600px;
  display: flex;
  margin-top: 10px;
  margin-left: 10px;
  padding: 10px;
}

.input-todo {
  width: 500px;
  height: 40px;
  text-indent: 1em
}

.add-button {
  margin-left: 20px;
  background: #a0ce97;
}

.items-container {
  display: flex;
  margin-left: 10px;
  padding: 10px;
  flex-direction: column;
}

.item {
  width: 600px;
  display: flex;
}

.item-text {
  margin-top: 10px;
  display: flex;
  align-items: center;
  background: #bbd9b5;
  text-indent: 0.5em;
  flex: 1;
}

.item-edit {
  margin-top: 10px;
  margin-left: 20px;
  background: cornflowerblue;
}

.item-remove {
  margin-top: 10px;
  margin-left: 20px;
  background: #d77272;
}

</style>
