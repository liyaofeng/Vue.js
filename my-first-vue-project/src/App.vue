<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <input type="text" v-model="newItem" v-on:keyup.enter="addNew()">
    <ul>
      <li v-for="item in items" v-text="item.label" :class="{finished: item.isFinished}" v-on:click="toggleFinish(item)">
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data () {
    return {
      title: 'This is a todo list!',
      items: [],
      // finishedClass: "finished"
      newItem: ""
    }
  },

  methods: {
    toggleFinish(item) {
      item.isFinished = !item.isFinished;
    },
    addNew() {
      if (this.newItem != "") {
        this.items.splice(0, 0, {
          label: this.newItem,
          isFinished: false
        })
        this.newItem = "";
      }
    }
  }
}
</script>

<style>
html {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

.finished {
  text-decoration: underline;
}

#app {
  color: #2c3e50;
  margin-top: -100px;
  max-width: 600px;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px
}
</style>
