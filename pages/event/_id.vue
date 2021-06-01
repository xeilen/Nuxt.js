<template>
  <h1>Event #{{ event.title }}</h1>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'Id',
  // props: {
  //   event: {
  //     type: Object,
  //     default: null,
  //   },
  // },
  async fetch({ store, error, params }) {
    try {
      await store.dispatch('events/fetchEvent', params.id)
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch event #' + params.id,
      })
    }
  },
  head() {
    return {
      title: 'Event #' + this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'What you need to know about event #' + this.event.title,
        },
      ],
    }
  },
  computed: {
    ...mapState('events', ['event']),
  },
}
</script>

<style scoped></style>
