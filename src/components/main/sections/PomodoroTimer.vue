<template>
  <div class="jumbotron">
    <div class="container">
      <img class="img-fluid rounded exercise-img"
           src="https://cdn.prod.openfit.com/uploads/2017/06/01150749/how-to-get-better-at-push-ups2.jpg"
           alt="Push-ups image">
      <h2>Push-ups</h2>
      <p>
        Description: lorem ipsum
      </p>
    </div>
    <div class="container">
      <div class="row">
        <div
          v-show="!isWorking"
          class="col-sm-4">WORKOUT TIME!
        </div>
        <count-down-timer class="col-sm-8" @finished="togglePomodoro"
                          :time="time"></count-down-timer>
      </div>
    </div>
  </div>
</template>
<script>
import CountDownTimer from './timer/CountDownTimer'
import {mapActions, mapGetters} from 'vuex'

export default {
  data () {
    return {
      isWorking: true,
      isShortBreak: false,
      isLongBreak: false,
      pomodoros: 0
    }
  },
  computed: {
    ...mapGetters({
      config: 'getConfig',
      statistics: 'getStatistics'
    }),
    time () {
      let minutes
      if (this.isWorking) {
        minutes = this.config.workingPomodoro
      } else if (this.isShortBreak) {
        minutes = this.config.shortBreak
      } else if (this.isLongBreak) {
        minutes = this.config.longBreak
      }
      return minutes * 60
    }
  },
  components: {
    CountDownTimer
  },
  methods: {
    ...mapActions(['setTotalPomodoros']),
    togglePomodoro () {
      this.setTotalPomodoros(this.statistics.totalPomodoros++)
      this.isWorking = !this.isWorking
      this.isShortBreak = this.isLongBreak = false
      if (this.isWorking) {
        return
      }
      this.pomodoros++
      console.log('aasd')
      this.isLongBreak = this.pomodoros %
        this.config.pomodorosTillLongBreak === 0
      this.isShortBreak = !this.isLongBreak
    }
  }
}
</script>
<style scoped lang="sass">
.exercise-img
  width: 350px
</style>
