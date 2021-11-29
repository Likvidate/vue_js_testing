<template>
  <div>
    <CountDown :timerTitle="title" :timerMessage="message" :year='2021' :month='11' :date='10' :hour='0' :minute='0' :second='0' :millisecond='0'/>
  </div>
</template>

<script>
// @ is an alias to /src
import CountDown from '@/components/countDown.vue'

export default {
  name: 'Home',
  components: {
    CountDown
  },
  data: function () {
    return {
      title: 'Time till your birthday',
      message: 'Happy birthday!!!'
    }
  }
}
</script>
