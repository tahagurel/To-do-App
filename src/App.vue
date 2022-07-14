<template>
  <div class="main">
    <div class="box">
    <h1>Todo App</h1>
    <div class="inputWrapper">
      <input v-model="todo" class="inputBox" placeholder="Add your new todo" type="text">
      <button :disabled="todo==''" class="addButton" @click="addToDoList">+</button>
    </div>
    <div class="doList">
      <div  v-for="(item,index) in todoList"
            :key="index"
            :class="item.isDone ? 'doneItem' : '' " class="doItem"
            @click="taskDone(index)">
        <div >{{item.name}}</div>
       <button @click="deleteTask(index)" class="deleteButton">x</button>
      </div>
    </div>
    <div class="infoWrapper">
      <span v-if="todoList.length"
       class="infoMessage">You have {{todoList.length}} pending tasks</span>
      <button :disabled="todoList.length<1" @click="clearAll" class="clearButton">Clear All</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      todo: '',
      todoList: [],
    };
  },
  methods: {
    addToDoList() {
      this.todoList.push({
        name: this.todo,
        isDone: false,
      });
      this.todo = '';
    },
    deleteTask(index) {
      this.todoList.splice(index, 1);
    },
    clearAll() {
      this.todoList = [];
    },
    taskDone(index) {
      const itemIsDone = this.todoList[index].isDone;
      this.todoList[index].isDone = !itemIsDone;
    },
  },
};
</script>

<style>
body{
  background: rgb(7,12,60);
  background: linear-gradient(90deg, rgba(7,12,60,1) 23%, rgba(255,42,0,1) 100%);
}
.main{
  margin: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.box{
  font-family: monospace;
  background-color: white;
  width: 400px;
  border-radius: 5px;
  padding: 10px 20px 0 20px;
}
@media only screen and (max-width: 600px) {
  .box{
    width: 310px;
  }
}
.inputWrapper{
  display: flex;
  justify-content: space-between;
}
.inputBox{
  width: 100%;
  margin-right: 5px;
  border:1px solid rgb(204, 202, 202);
  border-radius: 3px;
  text-indent: 7px;
}
.inputBox::placeholder {
  color: rgb(163, 161, 161);
  font-size: 15px;
  font-weight:400;
}
.addButton:disabled{
  background-color: rgb(228, 120, 120);
}
.clearButton:disabled{
  background-color: rgb(228, 120, 120);
}
.addButton{
  font-size: 25px;
  font-weight: bold;
  color: white;
  padding: 4px 12px 4px 12px;
  background-color: blueviolet;
  border:0;
  border-radius: 3px;
}
.doList{
  margin-top:12px;
}
.doItem{
  display: flex;
  justify-content: space-between;
  background-color: rgb(236, 234, 234);
  border-radius: 1px;
  font-size: 15px;
  align-items: center;
  padding-left: 8px;
  margin-bottom: 7px;
}
.deleteButton{
  font-size: 25px;
  font-weight: bold;
  color: white;
  padding: 4px 12px 4px 12px;
  background-color:#F44336;
  border:0;
  border-radius: 3px;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
.infoWrapper{
  margin-top: 25px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 20px;
}
.infoMessage{
  font-size: 15px;
}
.clearButton{
  background-color: blueviolet;
  border: 0;
  border-radius: 2px;
  padding: 8px 10px 8px 10px;
  color: white;
  font-size: 15px;
  font-weight:bold;
}
.doneItem{
  background-color:#4CAF50;
  color: white;
}
</style>
