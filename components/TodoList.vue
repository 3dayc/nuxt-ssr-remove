<template>
  <v-card class="mx-auto list" max-width="400" tile>
    <ul class="list-item">
      <li v-for="(todoItem, index) in todoItems" :key="index">
        <span
          :class="todoItem.completed"
          @click="doneToggle(todoItem, index)"
          >{{ todoItem.todo }}</span
        >
        <span class="close-btn" @click="removeItem(todoItem, index)">X</span>
      </li>
    </ul>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      todoItems: [
        // { todo: '축구', completed: '' },
        // { todo: '프리미어 리그', completed: 'done' },
        // { todo: '장보기', completed: '' },
      ],
    }
  },
  created() {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        this.todoItems.push(
          JSON.parse(localStorage.getItem(localStorage.key(i)))
        )
      }
    }
  },
  methods: {
    doneToggle(todoItem, index) {
      if (this.todoItems[index].completed === 'done') {
        this.todoItems[index].completed = ''
        localStorage.setItem(
          todoItem.todo,
          JSON.stringify({ todo: todoItem.todo, completed: '' })
        )
      } else {
        this.todoItems[index].completed = 'done'
        localStorage.setItem(
          todoItem.todo,
          JSON.stringify({ todo: todoItem.todo, completed: 'done' })
        )
      }
    },
    removeItem(todoItem, index) {
      localStorage.removeItem(todoItem.todo)
      this.todoItems.splice(index, 1)
    },
  },
}
</script>

<style scope>
.list {
  margin: 0 auto;
}
.list-item {
  list-style: none;
}
.list-item > li {
  padding: 0.5rem 1rem;
}
.list-item > li > span:first-child {
  cursor: pointer;
}
.list-item > li:first-child {
  padding-top: 1rem;
}
.list-item > li:last-child {
  padding-bottom: 1rem;
}
.close-btn {
  float: right;
  cursor: pointer;
}
.done {
  text-decoration: line-through;
  color: gray;
}
</style>
