<template>
  <div class="jumbotron">
    <div class="container">
      <img class="img-fluid rounded exercise-img" src="https://cdn.prod.openfit.com/uploads/2017/06/01150749/how-to-get-better-at-push-ups2.jpg" alt="Push-ups image">
      <h2>Push-ups</h2>
      <lead>
        Description: lorem ipsum
      </lead>
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
import config from './../../../config'
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
    time () {
      let minutes
      if (this.isWorking) {
        minutes = config.workingPomodoro
      } else if (this.isShortBreak) {
        minutes = config.shortBreak
      } else if (this.isLongBreak) {
        minutes = config.longBreak
      }
      return minutes * 60
    }
  },
  components: {
    CountDownTimer
  },
  methods: {
    togglePomodoro () {
      // toggle the working state
      this.isWorking = !this.isWorking
      // reset break states
      this.isShortBreak = this.isLongBreak = false
      // we have switched to the working state, just return
      if (this.isWorking) {
        return
      }
      // we have switched to the break state, increase the number of
      // pomodoros and choose between long and short break
      this.pomodoros++
      this.isLongBreak = this.pomodoros %
        config.pomodorosTillLongBreak === 0
      this.isShortBreak = !this.isLongBreak
    }
  }
}
</script>
<style scoped lang="sass">
.exercise-img
  width: 350px
</style>
