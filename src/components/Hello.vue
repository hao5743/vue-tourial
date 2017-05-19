<template>
  <div class="hello">
    <mt-button type="primary" @click.native="handleClick">按钮</mt-button>
  
    <h1>{{ msg }}</h1>
      <span v-bind:title="msg">
        鼠标悬停几秒钟查看此处动态绑定的提示信息！
      </span>
      <h2 v-if="seen">
        现在你看到我了
      </h2>
      <p v-for="item in todos">
        <todo-item v-bind:todo="item"></todo-item>
      </p>
      <p>{{ message }}</p>
      <button v-on:click="reverseMessage">逆转消息</button>
      <mt-button type="primary" @click.native="reverseMessage">逆转消息</mt-button>
      <p>
        {{ message }} <br>
        翻转计算属性：{{testComputed}}
      </p>
       <p>
        <input v-model="message">
        <mt-field label="用户名" placeholder="请输入用户名" v-model="message"></mt-field>
       </p>
       <p>{{msg | myfilter}}</p>

  </div>
</template>

<script>
import Vue from 'vue'
Vue.component('todo-item', {
  // todo-item 组件现在接受一个
  // "prop"，类似于一个自定义属性
  // 这个属性名为 todo。
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

export default {
  name: 'hello',
  data(){
    return {
      message: 'hello vue',
      msg: 'Welcome to Your Vue.js App',
      seen: true,
      todos: [
        { text: '学习 JavaScript' },
        { text: '学习 Vue' },
        { text: '整个牛项目' }
      ]
    }
  },
  methods: {
    reverseMessage: function(){
      this.message = this.message.split('').reverse().join('')
    }
  },
  filters: {
    myfilter: function(value){
      return value + 'zzz'
    }
  },
  computed: {
    // a computed getter
    testComputed: function(){
      // `this` points to the vm instance
      return this.message.split('').reverse().join('')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1,
  h2{
    font-weight: normal;
  }
  
  ul{
    list-style-type: none;
    padding: 0;
  }
  
  li{
    display: inline-block;
    margin: 0 10px;
  }
  
  a{
    color: #42b983;
  }
</style>
