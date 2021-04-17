<template>
  <div>{{statistics.totalPomodoros}}</div>
</template>
<script>
import {mapActions, mapGetters} from 'vuex'

export default {
  computed: {
    ...mapGetters({
      statistics: 'getStatistics'
    })
  },
  methods: {
    ...mapActions(['bindStatistics'])
  },
  created () {
    this.bindStatistics()
  }
}
</script>
<style scoped lang="sass">
</style>
