<template>
  <v-calendar
          v-model="value"
          :weekdays="weekday"
          type="month"
          :events="events"
          event-overlap-mode="stack"
          :event-overlap-threshold="30"
          :event-color="getEventColor"
          @change="getEvents"
        />
</template>

<script>
export default {
  name: 'advent',
  data: () => ({
    type: 'month',
    weekday: [0, 1, 2, 3, 4, 5, 6],
    value: '',
    events: [],
    colors: ['blue', 'indigo', 'deep-purple', 'cyan', 'green', 'orange', 'grey darken-1'],
  }),
  methods: {
    getEvents ({ start, end }) {
      const events = []

      const min = new Date(`${start.date}T00:00:00`)
      const max = new Date(`${end.date}T23:59:59`)
      const days = (max.getTime() - min.getTime()) / 86400000
      const eventCount = this.rnd(days, days + 20)

      for (let i = 0; i < eventCount; i++) {

        events.push({
          name: this.names[this.rnd(0, this.names.length - 1)],
          color: this.colors[this.rnd(0, this.colors.length - 1)],
          timed: false,
        })
      }

      this.events = events
    },
    getEventColor (event) {
      return event.color
    },
    rnd (a, b) {
      return Math.floor((b - a + 1) * Math.random()) + a
    },
  },
}
</script>

<style lang="css" scoped>
</style>
