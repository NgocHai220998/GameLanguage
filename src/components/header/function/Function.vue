<template>
  <section class="function">
    <Rank />
    <GotoLearn />
    <Position />
    <Recruit />
    <Courses />
  </section>
</template>

<script>

import Rank from './Rank'
import GotoLearn from './GotoLearn'
import Position from './Position'
import Recruit from './Recruit'
import Courses from './Courses'

export default {
  name: 'FunctionHeader',
  data () {
    return {
    }
  },
  components: {
    Rank,
    GotoLearn,
    Position,
    Recruit,
    Courses
  }
}
</script>

<style lang="scss" scoped>
  .function {
    display: flex;
    flex-wrap: wrap;
  }
</style>
