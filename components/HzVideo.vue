<template>
  <view
    class="wrap-hz-video"
    :style="{ width: `${width * 2}rpx`, height: `${height * 2}rpx` }"
  >
    <video :id="id" class="video" :src="source" />
    <image :src="image" class="image" />
    <view @tap.stop="playerVideo" class="mark">
      <view
        class="icon hzfont icon-player"
        :style="{ 'font-size': `${iconSize * 2}rpx` }"
      />
    </view>
  </view>
</template>

<script>
export default {
  name: "HzVideo",

  props: {
    source: {
      required: true,
      type: String
    },
    image: {
      required: true,
      type: String
    },
    width: {
      type: Number,
      default() {
        return 150;
      }
    },
    height: {
      type: Number,
      default() {
        return 150;
      }
    },
    iconSize: {
      type: Number,
      default() {
        return 60;
      }
    }
  },
  data() {
    return {
      id: this.generateUUID()
    };
  },
  methods: {
    playerVideo() {
      const videoContext = uni.createVideoContext(this.id, this);
      videoContext.requestFullScreen();
      videoContext.play();
    },

    /**
     * 生成一个uuid
     */
    generateUUID() {
      var d = new Date().getTime();
      var uuid = "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx".replace(
        /[xy]/g,
        function(c) {
          var r = (d + Math.random() * 16) % 16 | 0;
          d = Math.floor(d / 16);
          return (c == "x" ? r : (r & 0x7) | 0x8).toString(16);
        }
      );
      return uuid;
    }
  }
};
</script>

<style lang="scss" scoped>
.wrap-hz-video {
  display: inline-block;
  position: relative;
  .video {
    width: 0;
    height: 0;
  }
  .image {
    width: 100%;
    height: 100%;
  }
  .mark {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgba(0, 0, 0, 0.6);
    .icon {
      color: #fff;
    }
  }
}
</style>
