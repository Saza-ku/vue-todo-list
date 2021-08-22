<template>
  <input v-model="inputValue">
  <button v-on:click="handleClick">
    ToDo を追加
  </button>
  <ul>
    <li v-for="todo in todoItems"
      v-bind:key="todo.id"
      v-on:click="todo.done = !todo.done">
      <span v-if="todo.done">✔︎</span>
      {{ todo.text }}
    </li>
  </ul>
</template>

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
      ]
    }
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
    }
  }
}
</script>