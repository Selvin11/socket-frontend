<template>
  <div class="home">
    <!-- <img src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- <el-input v-model="input" @keyup.enter="submitName" placeholder="请输入内容"></el-input> -->
    <input v-model="input" @keyup.enter="submitName" placeholder="请输入内容" />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import io from 'socket.io-client'
// 连接服务器
const socket = io('http://localhost:3000')

export default {
  name: 'home',
  components: {
    HelloWorld
  },
  data () {
    return {
      input: ''
    }
  },
  created () {
    // 监听服务器触发的'news'事件
    socket.on('news', function (data) {
      console.log(data)
      // 客户端向服务器端发起其它事件，并传递数据，服务端监听此事件，即可获取到数据
      socket.emit('my other event', { my: 'data' })
    })
  },
  methods: {
    submitName () {
      socket.emit('submitName', { name: this.input })
    }
  }
}
</script>
