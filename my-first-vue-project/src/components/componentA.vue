<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>{{ msgFromFather }}</h1>
    <button v-on:click="onClickMe">open mouse!</button>
    <p>father dispatch me: {{ newMsgFromFather }}</p>
  </div>
</template>

<script>
export default {
  data () {
    return {
      msg: "hello from component a!",
      fatherMsg: "",
      newMsgFromFather: ""
    }
  },
  props: ["msgFromFather"],
  events: {
    'on-add-new': function (msg) {
      console.log("hahahaha");
      this.fatherMsg = msg;
    },
    'child-msg': function (msg) {
      this.fatherMsg = msg;
    }
  },
  methods: {
    onClickMe() {
      console.log(this.msgFromFather);
      this.$emit("child-tell-me-something", this.msg);
    }
  }
}
</script>

<style>
h1 {
  color: #42b983;
}
</style>
