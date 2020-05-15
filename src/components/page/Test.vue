<template>
  <div class="main">
    <el-row>
      <el-button type="primary" plain @click='setParams'>设置流参数</el-button>
      <el-button type="success" plain  @click='beginPush'>开始推流</el-button>
      <el-button type="danger" plain  @click='endPush'>关闭推流</el-button>
    </el-row>
  </div>
</template>

<script>
    export default {
        name: "Test",
      data() {
        return {
          path: "ws://172.18.27.88:8060",
          form: { // 表单
            action: '',
            data: {
              streamUrl: '',
              outResolution: '',
              fps: '',
              bitRate: ''
            }
          }
        }
        },
      mounted () {
        // 初始化
        this.init()
        console.log("let a = 1")
      },
      methods: {
        init() {
          if(typeof(WebSocket) === "undefined"){
            alert("您的浏览器不支持socket")
          }else{
            // 实例化socket
            this.socket = new WebSocket(this.path)
            // 监听socket连接
            this.socket.onopen = this.open
            // 监听socket错误信息
            this.socket.onerror = this.error
            // 监听socket消息
            this.socket.onmessage = this.getMessage
          }
        },
        open: function () {
          console.log("socket连接成功")
        },
        error: function () {
          console.log("连接错误")
        },
        getMessage: function (msg) {
          console.log(msg.data)
          alert(msg.data)
        },
        setParams: function () {
          let params = this.form;
          params.action = 2;
          params.data.streamUrl = "rtmp://26267431cv.zicp.vip:25670/hls";
          params.data.outResolution = "1920x1080";
          params.data.fps = 30;
          params.data.bitRate = 2500;
          this.socket.send(JSON.stringify(params))
        },
        beginPush: function () {
          let params = this.form;
          params.action = 1;
          this.socket.send(JSON.stringify(params))
        },
        endPush: function () {
          let params = this.form;
          params.action = 0;
          this.socket.send(JSON.stringify(params))
        },
        close: function () {
          console.log("socket已经关闭")
        }
      },
      destroyed () {
        // 销毁监听
        this.socket.onclose = this.close
      }
    }
</script>

<style scoped>

</style>
