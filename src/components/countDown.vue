<template>
  <div style="top: 30%; left: 20%; width: 60%; position: absolute" v-if='loaded'>
    <h1 v-if='!timerDone'>{{timerTitle}}</h1>
    <h1 v-else>{{timerMessage}}</h1>
    <div class="grid-container">
      <div class="item1">{{displayDays}}</div>
      <div class="item2">{{displayHours}}</div>
      <div class="item3">{{displayMinutes}}</div>  
      <div class="item4">{{displaySeconds}}</div>
      <div class="item5">Days</div>
      <div class="item6">Hours</div>
      <div class="item7">Minutes</div>
      <div class="item8">Seconds</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CountDown',
  props: { 
    timerTitle: null,
    timerMessage: null,
    year: null, 
    month: null, 
    date: null, 
    hour: null, 
    minute: null, 
    second: null, 
    millisecond: null 
  },
  data: function () {
    return {
      displayDays: 0,
      displayHours: 0,
      displayMinutes: 0,
      displaySeconds: 0,
      loaded: false,
      timerDone: false
    }
  },
  computed: {
    _seconds: () => 1000,
    _minutes () {
      return this._seconds * 60
    },
    _hours () {
      return this._minutes * 60
    },
    _days () {
      return this._hours * 24
    },
    end () {
      return new Date(
        this.year, this.month, this.date, this.hour, this.minute, this.second, this.millisecond
      )
    }
  },
  mounted () {
    this.showTime()
  },
  methods: {
    format (number) {
      return number < 10 ? '0' + number : number
    },
    showTime () {
      const timer = setInterval(() => {
        const now = new Date()
        const distance = this.end.getTime() - now.getTime()

        if (distance < 0) {
          clearInterval(timer)
          this.timerDone = true
          return
        }

        const days = Math.floor((distance / this._days))
        const hours = Math.floor((distance % this._days) / this._hours)
        const minutes = Math.floor((distance % this._hours) / this._minutes)
        const seconds = Math.floor((distance % this._minutes) / this._seconds)

        this.displayMinutes = this.format(minutes)
        this.displaySeconds = this.format(seconds)
        this.displayHours = this.format(hours)
        this.displayDays = this.format(days)
        this.loaded = true
      }, 1000)
    }
  }
}
</script>


<style>
.grid-container {
  display: grid;
  grid-template-columns: auto auto auto auto;
  grid-gap: 20px 50px;
  background-color: lightpink;
  padding: 10px;
}

.grid-container > div {
  background-color: pink;
  text-align: center;
  padding: 20px 0;
  font-size: 30px;
}
</style>

