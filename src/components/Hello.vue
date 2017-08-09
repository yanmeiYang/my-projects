<template>
  <div class="hello">
    <input v-model="msg" v-on:keyup.enter="addTodo"/>
    <ul>
      <li v-for="todo in todos">
        <span>{{todo.text}}</span>
        <button v-on:click='removeTodo($index)'>X</button>
      </li>
    </ul>
    <button clsss="btn btn-primary btn-sm" v-on:click="greet">测试在js中调用方法</button>
    <hr>
    <word </word>
  </div>
</template>

<script>
import Word from './Word'
export default {
  name: 'hello',
  components: {
    'word': Word
  },
  data () {
    return {
      msg: '',
      todos: [
        {text: 'add some1 test Changelog'}
      ]
    }
  },
  methods: {
    addTodo () {
      var text = this.msg.trim()
      if (text) {
        this.todos.push({text: text})
        this.msg = ''
      }
    },
    removeTodo (index) {
      this.todos.splice(index, 1)
    },
    greet (event) {
      this.msg = event.target.tagName
      window.alert(this.msg)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
