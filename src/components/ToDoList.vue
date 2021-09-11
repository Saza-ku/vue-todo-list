<template>
  <button v-on:click="handleClick">
    ToDo を追加
  </button>
  <input v-model="inputValue">
  <input
    v-model="filterValue"
    placeholder="フィルタテキスト">
  <ul>
    <to-do-item
      v-for="todo in filteredTodoItems"
      v-bind:key="todo.id"
      v-bind:text="todo.text"
      v-bind:done="todo.done"
    />
  </ul>
</template>

<style>
.todo-item.done {
  background-color: #3fb983;
}
</style>

<script>
import ToDoItem from './ToDoItem.vue'
export default {
  components: { ToDoItem },
  data() {
    return {
      inputValue: '',
      todoItems: [
        { 
          id: 1,
          done: false,
          text: 'Go out to sea'
        },
        { id: 2,
          done: false,
          text: 'Invite the first member'
        }
      ],
      filterValue: '',
    }
  },
  computed: {
    filteredTodoItems() {
      if (!this.filterValue) {
        return this.todoItems
      }
      return this.todoItems.filter((todo) => {
        return todo.text.includes(this.filterValue)
      })
    },
  },
  methods: {
    handleClick() {
      // todo をリストに追加
      this.todoItems.push({
        id: this.todoItems.length + 1,
        done: false,
        text: this.inputValue
      })
      // 入力をクリア
      this.inputValue = ''
    },
  }
}
</script>