<template>
  <div>
    <div style="margin:10px 0">
      <el-button type="primary" @click="keepLiveVideo">开始直播</el-button>
      <el-button type="primary" @click="stopLiveVideo">停止直播</el-button>
      <el-button type="primary" @click="toHome">
        返回首页
      </el-button>
    </div>
    <video ref="videoElement" controls autoplay width="100%" height="450px" poster="" @pause="handlePause" @play="handlePlay">Your browser is too old which doesn't support HTML5 video.</video>
  </div>
</template>

<script>
import flvjs from 'flv.js'

export default {
  name: 'School',
  props: {
    types: {
      type: String,
      default: 'flv'
    },
    url: {
      type: String,
      default: 'http://39.106.160.150:1936/live/123456.flv'
    }
  },
  data() {
    return {
      flvPlayer: null
    }
  },
  watch: {
    url() {
      if (this.flvPlayer) {
        this.flvPlayer.destroy()
      }
      this.createVideo()
    }
  },
  mounted() {
  },
  methods: {
    keepLiveVideo() {
      if (this.flvPlayer == null) {
        const videoElement = this.$refs.videoElement
        this.flvPlayer = flvjs.createPlayer({
          type: this.types,
          url: this.url
        })
        this.flvPlayer.attachMediaElement(videoElement)
        this.flvPlayer.load()
      }
    },
    stopLiveVideo() {
      if (this.flvPlayer) {
        this.flvPlayer.destroy()
        this.flvPlayer = null
      }
    },
    handlePause() {
      // if (this.flvPlayer) {
      //     this.flvPlayer.destroy()
      //     this.flvPlayer = null
      // }
    },
    handlePlay() {
      if (this.flvPlayer == null) {
        const videoElement = this.$refs.videoElement
        this.flvPlayer = flvjs.createPlayer({
          type: this.types,
          url: this.url
        })
        this.flvPlayer.attachMediaElement(videoElement)
        this.flvPlayer.load()
      }
    },
    toHome() {
      this.$router.push('/')
    }
  }
}
</script>
