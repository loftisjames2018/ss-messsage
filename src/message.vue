<template>
  <transition name="message">
    <span class="message-container" v-if="messageShow">
      <span class="message-icon" :class="messageIconClass"></span>
      <span class="message-text">
        <span v-html="placeHolder"></span>
      </span>
    </span>
  </transition>
</template>

<script>
  import {mapGetters, mapActions} from 'vuex'

  export default {
    methods: {
      messageClose() {
        this.$emit('messageClose');
      }
    },
    computed: {
      ...mapGetters({
        messageShow: 'getMessageShow',
        placeHolder: 'getPlaceHolder',
        hideTime: 'getHideTime',
        kind: 'getKind'
      }),
      messageIconClass() {
        return {
          'message-icon--success': this.kind === 'success',
          'message-icon--warning': this.kind === 'warning',
          'message-icon--error': this.kind === 'error'
        }
      }
    },
    watch: {
      messageShow(val) {
        if (val) {
          setTimeout(() => {
            this.messageClose();
          }, this.hideTime);
        }
      }
    }
  }
</script>

<style lang="less" scoped>
  .message-container {
    position: fixed;
    top: 40px;
    left: 50%;
    transform: translateX(-50%);
    display: inline-block;
    background-color: #fff;
    box-shadow: 0 2px 8px rgba(0, 0, 0, .16);
    z-index: 100010;
    border-radius: 4px;

    .message-icon {
      float: left;
      width: 16px;
      height: 16px;
      margin: 10px 16px 10px 24px;
      background-image: url(./img/message_icon.svg);
    }

    .message-icon--success {
      background-position: 0px -16px;
    }
    .message-icon--error {
      background-position: -16px -16px;
    }
    .message-icon--warning {
      background-position: -32px -16px;
    }

    .message-text {
      float: left;
      font-size: 14px;
      color: #626262;
      margin: 10px 24px 10px 0;
    }

  }

  .message-enter-active, .message-leave-active {
    transition: opacity .5s, transform .5s;
  }
  .message-enter, .message-leave-active {
    opacity: 0;
    transform: translate(-50%,-24px);
  }
</style>
