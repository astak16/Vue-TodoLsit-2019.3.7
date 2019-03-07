<template>
  <div>
    <input type="text" v-model.trim="msg" @keyup.enter="push">
    <ul>
      <li v-for="(item, index) in list" @click="deleteItem(index)">
        {{index}}{{item.name}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      msg: "",
      list: []
    }
  },
  methods: {
    push () {
      this.list.push({name: this.msg})
      this.msg = ""
    },
    deleteItem (index) {
      this.list.splice(index, 1)
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
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
