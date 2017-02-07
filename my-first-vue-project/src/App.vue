<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <input type="text" v-model="newItem" v-on:keyup.enter="addNew()">
    <ul>
      <li v-for="item in items" v-text="item.label" :class="{finished: item.isFinished}" v-on:click="toggleFinish(item)">
      </li>
    </ul>
    <p>child tell me: {{ childWords }}</p>
    <component-a id="componentsa" msg-from-father="you die!" v-on:child-tell-me-something="listenToMyBoy"></component-a>
  </div>
</template>

<script>
import Store from "./storage.js"
import ComponentA from "./components/componentA.vue"
export default {
  data () {
    return {
      title: 'This is a todo list!',
      items: Store.fetch(),
      // finishedClass: "finished"
      newItem: "",
      childWords: ""
    }
  },

  components: {
    ComponentA
  },

  watch: {
    "items": {
      handler(items) {
        Store.save(items)
      },
      deep: true
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
        });
        console.log(this.newItem);
        ComponentA.newMsgFromFather = this.newItem;
        document.getElementById('componentsa').newMsgFromFather = this.newItem;
        this.$dispatch("on-add-new", this.newItem);
        this.$dispatch('child-msg', this.newItem);
        this.newItem = "";
      }
    },
    listenToMyBoy(msg) {
      this.childWords = msg;
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
