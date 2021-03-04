
<template>
  <div id="app">
    <div class="board" v-for="(board,indexBoard) in boards" :key="indexBoard">
      <div class="header-board">
        <h1 class="title-board">{{board}}</h1>
        <button v-on:click="removeBoard(indexBoard)" class="btn btn-remove">delete</button>
      </div>
      <div class="content-todo"  v-for="(todo,indexTodo) in todos" :key="indexTodo" >
        <div v-if="todo.type === board" class="card">
          <p class="text-todo">{{todo.title}}</p>
          <div class="button-list">
            <button style="margin-right:10px" v-if="indexBoard !== boards.length - 1" v-on:click="move(indexBoard,indexTodo)" class="btn btn-move">move</button>
            <button v-on:click="remove(indexTodo)" class="btn btn-remove">remove</button>
          </div>
        </div>
      </div>
      <div v-if="addCard === board" class="input-card">
        <input type="text" v-model="inputTodo" >
        <button v-on:click="addItem(board)" class="btn btn-save">Add Card</button>
        <button class="btn-close" v-on:click="closeAddCard()">x</button>
      </div>
      <div v-if="addCard !== board" class="add-card" v-on:click="showAddCard(board)" >
        <p>+ Add another card</p>
      </div>
    </div>
    <div @click="addBoard()" class="add-board">
      <p>+ Add another list</p>
    </div>
  </div>
</template>
<script>

export default {
  name: 'App',
  data:()=>{
    return{
      todos:[

      ],
      inputTodo:'',
      boards:["Todo"],
      addCard:""
    }
  },
  methods:{
    addItem:function (type){
      let title = this.inputTodo
      this.todos.push({
        title,
        type
      })
      this.inputTodo = ""

    },
    move: function(idBoard,indexTodo){
      if (idBoard!== this.boards.length-1){
        this.todos[indexTodo].type = this.boards[idBoard+1]
      }
    },
    showAddCard:function(board){
      this.addCard = board
    },
    remove:function(id) {
      this.todos.splice(id,1)
    },
    removeBoard:function(id) {
      let data = []
      for (let i = 0; i < this.todos.length; i++) {
        if (this.todos[i].type!== this.boards[id]) {
          data.push(this.todos[i])
        }
      }
      this.todos = data
      this.boards.splice(id,1)

    },
    addBoard:function(){
      let board = prompt("Nama Board");
      this.boards.push(board)
    },
    closeAddCard:function() {
      this.addCard = ''
    }
  }
}
</script>

<style>
body{
  background: #0079bf;

}
.header-board{
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.header-board h1{
  margin-left: 20px;
}

.btn-save{
  background-color: #5aac44;
}

.header-board button{
  height: 100%;
  padding: 8px 10px;
  margin-right: 10px;
}
.add-board{
  margin-top: 20px;
  min-width: 272px;
  border-radius: 4px;
  background: #ebecf0;;
  padding: 10px;
  height: 100%;
  margin-bottom: 20px;
  margin-left: 10px;
}
.add-board:hover{
    background-color: #c6cbd3;
    cursor: pointer;
}

#app {
  display: flex;
}
*{
  margin:0;
  padding:0;
}

.board{
  margin-top: 20px;
  min-width: 272px;
  border-radius: 4px;
  background: #ebecf0;
  height: 100%;
  margin-bottom: 20px;
  margin-left: 10px;
}

.add-card{
  padding: 4px 10px;
  margin: 10px 10px;
}

.add-card:hover{
  background: #aaa;
  cursor: pointer;
}

.btn-move{
  background: #0079bf;
}
.input-card{
  margin: 10px;
}
.input-card input{
  display: block;
  width: 96%;
  border-radius: 4px;
  padding: 10px 0px 40px 10px;
  border: none;
  margin-bottom: 15px;
}
.btn{
  padding: 6px;
  border-radius: 4px;
  border: none;
  color: #fff;
}
.btn-remove{
  background: #f3442c;
}
.btn-close{
  color: #777;
  font-size: 22px;
  border: none;
  padding: 0px 10px;
  margin-left: 5px;
}

.text-todo{
  font-size: 17px;
}

.title-board{
  text-align: center;
  margin-top: 10px;
  margin-bottom: 10px;
}

.card{
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: whitesmoke;
  padding: 10px;
  margin: 10px 10px;
  border-radius: 4px;
}

</style>
