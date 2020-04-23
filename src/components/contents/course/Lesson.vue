<template>
  <section class="lesson-detail">
    <div :style="{ maxHeight: maxHeight + 'px' }" class="left">
      <div v-for="(word, i) in lesson.words" :key="i" class="item">
        <span class="vocabulary btn">{{ i + 1}}. {{ word.vocabulary }}</span>
        <span class="explain btn">{{ word.explain }}</span>
        <a-tooltip>
          <template slot="title">
            Thêm vào danh sách học của bạn
          </template>
          <a-button @click="addWordFromCourse(word)" type="primary" size="small" class="btn-plus"><a-icon type="plus" /></a-button>
        </a-tooltip>
      </div>
    </div>
    <div class="right">
      <div class="group-button">
        <div>
          <a-button type="primary" class="btn-plus background">Học ngay</a-button>
        </div>
      </div>
    </div>
  </section>
</template>
<script>

export default {
  name: 'LessonComponent',
  data () {
    return {
      user: null,
      windowHeight: null
    }
  },
  props: ['socket', 'lesson'],
  methods: {
    connectSocket () {
      this.socket.on('addWordFromCourseDone', (data) => {
        this.$message.success('Thêm thành công')
      })
    },
    addWordFromCourse (word) {
      this.socket.emit('clientAddWordFromCourse', {
        token: this.user.token,
        vocabulary: word.vocabulary,
        explain: word.explain
      })
    }
  },
  computed: {
    maxHeight () {
      return (this.windowHeight > 700) ? 350 : 250
    }
  },
  beforeMount () {
    this.user = JSON.parse(localStorage.getItem('user'))
    this.windowHeight = window.innerHeight
    this.connectSocket()
  }
}
</script>

<style lang="scss" scoped>
  .lesson-detail {
    display: flex;
    justify-content: space-between;
    .right {
      max-width: 150px;
      min-width: 150px;
    }
    .left {
      width: 100%;
      overflow: scroll;
      background-color: rgba(0, 0, 0, 0.75);
      .item {
        padding: 12px 15px 7px 15px;
        border-bottom: 1px solid white;
        .vocabulary {
          display: inline-block;
          width: 200px;
          max-width: 200px;
          color: white;
          font-size: 20px;
        }
        .explain {
          display: inline-block;
          width: 310px;
          max-width: 310px;
          color: white;
          font-size: 20px;
        }
        .btn-plus {
          width: 70px;
          position: relative;
          bottom: 8px;
        }
        &:hover {
          box-shadow: 1px 1px 1px green, 1px 1px 5px green, 1px 1px 25px red;
          cursor: pointer;
        }
      }
    }
    .right {
      text-align: center;
      .group-button {
        text-align: center;
      }
    }
  }
</style>
