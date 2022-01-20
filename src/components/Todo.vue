<template>
  <div class="todo-component">
    <form @submit.prevent="addTodo()" class="new-todo">
      <input
        autocomplete="off"
        type="text"
        v-model="todoText"
        placeholder="Yeni Todo"
        id="add-todo-input"
      />
    </form>
    <hr />
    <div class="todo-list">
      <div v-for="todo in todos" :key="todo.id" id="single-todo">
        <input v-if="todo.id === updateId" v-model="todo.todo" />
        <span v-else class="todoText">
          <del v-if="todo.isSuccess === true">{{ todo.todo }}</del>
          <p v-else>{{ todo.todo }}</p>
        </span>
        <div class="actions">
          <button
            v-if="todo.isSuccess === false"
            @click="onCompleteHandle(todo)"
            class="complete-button"
          >
            Tamamla
          </button>
          <button
            v-else
            class="not-complete-button"
            @click="onNotCompleteHandle(todo)"
          >
            Tamamlanmadı
          </button>
          <button @click="onHandleDelete(todo)">Sil</button>
          <button v-if="todo.id !== updateId" @click="updateTodo(todo)">
            Güncelle
          </button>
          <button v-else @click="onHandleSaveTodo(todo)">Kaydet</button>
          <button v-if="todo.id === updateId" @click="onCancelUpdate()">İptal</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      todoText: "",
      initialId: 1,
      todos: [],
      updateId: null,
    };
  },
  methods: {
    addTodo() {
      if (this.todoText.trim().length !== 0) {
        this.todos.push({
          id: this.initialId,
          todo: this.todoText,
          isSuccess: false,
        });
        this.initialId++;
        this.todoText = "";
      }
    },
    onHandleDelete(product) {
      this.todos = this.todos.filter((todo) => todo.id !== product.id);
    },
    updateTodo(todo) {
      this.updateId = todo.id;
    },
    onCompleteHandle(todo) {
      todo.isSuccess = true;
    },
    onNotCompleteHandle(todo) {
      todo.isSuccess = false;
    },
    onHandleSaveTodo(todo){
        this.todos.filter(t => t.id === todo.id)[0] = todo;
        this.updateId = null;
    },
    onCancelUpdate(){
        this.updateId = null;
    }
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}
.todo-component {
  width: 400px;
  min-height: 500px;
  border-radius: 8px;
  background-color: #ecb390;
}
.new-todo {
  height: 30px;
  margin: 20px;
}

#add-todo-input {
  width: 100%;
  height: 30px;
  border: none;
  outline: none;
  border-radius: 3px;
  border: 1px solid lightgray;
  font-size: 18px;
}

.todo-list {
  width: 100%;
}
#single-todo {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 35px;
  padding: 10px;
  margin: 5px;
}

.todoText {
  font-family: sans-serif;
}
</style>