<template>
  <div>
    <h1>Events</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script>
import EventCard from '../components/EventCard'
export default {
  components: { EventCard },
  async asyncData({ $axios, error }) {
    try {
      const response = await $axios.get('http://localhost:3000/events')
      return {
        events: response.data,
      }
    } catch (e) {
      error({
        statusCode: 503,
        message:
          'Unable to fetch events at this time. Please try again later ' +
          e.message,
      })
    }
  },
  head() {
    return {
      title: 'Event Listing',
    }
  },
}
</script>
