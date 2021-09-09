<template>
  <button v-on:click="handleClick">
    ToDo を追加
  </button>
  <input v-model="inputValue">
  <input
    v-model="filterValue"
    placeholder="フィルタテキスト">
  <ul>
    <li
      v-for="todo in filterdTodoItems"
      v-bind:key="todo.id"
      class="todo-item"
      v-bind:class="{'done': todo.done}"
      v-on:click="todo.done = !todo.done">
      <span v-if="todo.done">✔︎</span>
      {{ todo.text }}
    </li>
  </ul>
</template>

<style>
.todo-item.done {
  background-color: #3fb983;
}
</style>

<script>
export default {
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
    filterdTodoItems() {
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